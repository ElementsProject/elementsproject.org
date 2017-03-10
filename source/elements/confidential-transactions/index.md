---
title: Confidential Transactions
description: Preserve security while simultaneously obscuring transaction values.
image: /img/confidential-transactions.svg
source: https://github.com/ElementsProject/elementsproject.github.io/blob/master/source/elements/confidential-transactions/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/master/source/elements/confidential-transactions/index.md
---

One of the most powerful new features being explored in Elements is Confidential
Transactions.  This keeps the amounts transferred visible only to participants
in the transaction (and those they designate), while still guaranteeing that no
more coins can be spent than are available in a cryptographic way.

This goes a step beyond the usual privacy offered by Bitcoin's blockchain, which
relies purely on pseudonymous (but public!) identities.  This matters, because
insufficient financial privacy can have serious security and privacy
implications for both commercial and personal transactions. Without adequate
protection, thieves and scammers can focus their efforts on known high-value
targets, competitors can learn business details, and negotiating positions can
be undermined.

<div class="ui message">
  <h4 class="header">Did you know?</h4>
  <p>By sharing the blinding key used in the construction of a single confidential transaction, users can share access to the transaction's details.</p>
</div>

#### In Practice
The payment flow when using the Confidential Transactions Element is nearly
identical to Bitcoin Core on the surface:

```
elements-cli getnewaddress
XoR8jNLkTr7VmSTRxWh1pizJgcXX6cuDD3nxNpeGAEmvitWuZ6eDzJcnVbUCtko6LAxVvqTuPhFuXTJq

elements-cli sendtoaddress XoR8jNLkTr7VmSTRxWh1pizJgcXX6cuDD3nxNpeGAEmvitWuZ6eDzJcnVbUCtko6LAxVvqTuPhFuXTJq 0.005
82b2c5122207e5f33e7adadc6a4aab16a170e16028f0b0cf2c04f9d17d6f0321
```

The key difference from Bitcoin is the addition of cryptographic privacy. These
transactions differ in that the the amounts transferred are kept visible only to
participants in the transaction (and those they designate).

#### Confidential Addresses
The most visible implication of Confidential Transactions is the introduction of
a new default address type, confidential addresses:

```
XoR8jNLkTr7VmSTRxWh1pizJgcXX6cuDD3nxNpeGAEmvitWuZ6eDzJcnVbUCtko6LAxVvqTuPhFuXTJq
```

The most obvious differences are that it starts with ``XoR`` and is longer than
usual. This is due to the inclusion of a public blinding key prepended to the
base address. In the Liquid wallet the blinding key is derived by using the
wallet's master blinding key and unblinded P2PKH address. Therefore the receiver
alone can decrypt the sent amount, and can hand it to auditors if needed. On the
sender's side, ``sendtoaddress`` will use this pubkey to transmit the necessary
info to the receiver, encrypted, and inside the transaction itself. The sender's
wallet will also record the amount and hold this in the ``wallet.dat`` metadata
as well as the ``audit.log`` file.

```
elements-cli validateaddress XoR8jNLkTr7VmSTRxWh1pizJgcXX6cuDD3nxNpeGAEmvitWuZ6eDzJcnVbUCtko6LAxVvqTuPhFuXTJq
{
  "isvalid": true,
  "address": "XoR8jNLkTr7VmSTRxWh1pizJgcXX6cuDD3nxNpeGAEmvitWuZ6eDzJcnVbUCtko6LAxVvqTuPhFuXTJq",
  "scriptPubKey": "76a91448a67bbdaf57b6f55b50f02fcaacfa079900853588ac",
  "confidential_key": "02483237addc73befdb9b851f948c1488cbb7cf1a59ba8af36be1c479e0f6e8bc7",
  "unconfidential": "QTE8CaT6FcJEqkCR4ZGdoUJfas57eDqY6q",
  "ismine": true,
  "iswatchonly": false,
  "isscript": false,
  "pubkey": "0347b013d415f7dc964cfadd0bb0627c48ae6ae27a58cdd37d71990eaf8f38c60c",
  "iscompressed": true,
  "account": ""
}
```

As you can see the unconfidential P2PKH address starts with a `Q`. P2SH start
with `H`. Most RPC calls outside of ``getnewaddress`` (e.g., ``listunspent``)
will return the unblinded version of addresses. If you provide an unconfidential
address to ``validateaddress`` it will show the confidential address.

You **must** use the confidential address in ``sendtoaddress``, ``sendfrom``,
``sendmany`` and ``createrawtransaction`` if you want to create confidential
transactions. Therefore, when you want to receive confidential transactions you
must give the *confidential* address to the sender. For all other RPC's except
``dumpblindingkey`` it does not matter whether the confidential or
unconfidential address is provided.

In order to execute a third-party audit of transaction amounts, the blinding key
can be exported by the receiver and passed on to the auditor.

```
elements-cli dumpblindingkey XoR8jNLkTr7VmSTRxWh1pizJgcXX6cuDD3nxNpeGAEmvitWuZ6eDzJcnVbUCtko6LAxVvqTuPhFuXTJq
5fd02f714d52b68bbbfef3b8e6d83be646fad1de5150e83d26a28496e00a2146
```

The auditor may then import the address and blinding key with
``importblindingkey`` to observe watch-only amounts.

```
elements-cli importaddress XoR8jNLkTr7VmSTRxWh1pizJgcXX6cuDD3nxNpeGAEmvitWuZ6eDzJcnVbUCtko6LAxVvqTuPhFuXTJq
elements-cli listtransactions "*" 1 0 true
[
]
elements-cli importblindingkey XoR8jNLkTr7VmSTRxWh1pizJgcXX6cuDD3nxNpeGAEmvitWuZ6eDzJcnVbUCtko6LAxVvqTuPhFuXTJq 5fd02f714d52b68bbbfef3b8e6d83be646fad1de5150e83d26a28496e00a2146
elements-cli listtransactions "*" 1 0 true
[
  {
    "involvesWatchonly": true,
    "account": "",
    "address": "QTE8CaT6FcJEqkCR4ZGdoUJfas57eDqY6q",
    "category": "receive",
    "amount": 0.00500000,
    "label": "",
    "vout": 1,
    "confirmations": 35,
    "blockhash": "708f969b4fb1c705b82fa3ed309abc7a3d9b0e87aa6e5d17542bb7ee04c8e1f1",
    "blockindex": 1,
    "blocktime": 1488223140,
    "txid": "82b2c5122207e5f33e7adadc6a4aab16a170e16028f0b0cf2c04f9d17d6f0321",
    "walletconflicts": [
    ],
    "time": 1488223140,
    "timereceived": 1488225018,
    "bip125-replaceable": "no",
    "blindingfactors": "0000000000000000000000000000000000000000000000000000000000000000:71260137a80039dd8cee330d9f7bba625697dc53098cf54d625242946f26997b:"
  }
]
```

The ``createrawtransaction`` API in Liquid works similar to Bitcoin's raw
transactions with the following differences:

1. The intent to create a confidential output is indicated by using a confidential address for the destination.
2. The ``createrawtransaction`` RPC has the additional key ``nValue`` per input which must be set to the value of the input. The value can be determined for example with the ``listunspent`` RPC.
3. After calling ``createrawtransaction`` the user must call ``blindrawtransaction`` on the transaction if a confidential input or output address is involved.
4. If at least one of the inputs is confidential, at least one of the outputs must be confidential. Note that it is perfectly fine to create a 0-valued confidential output if otherwise there would be no confidential output.
5. If all inputs are unconfidential, the number of confidential outputs must be ``0`` or ``>= 2``. Again, it's fine to create a 0-valued confidential output.

The following example spends a confidential and an unconfidential output and
creates a confidential and unconfidential output. Due to the size of the
transaction it is not displayed here but saved in the variable ``TX``

```
TX=`elements-cli createrawtransaction '[{"txid": "421079661b117b659af3431096ce2118043396e3647e523e413cd626fa798df7", "vout": 0, "nValue": 0.001}, {"txid": "17aa26d29582a9a26f02033918aaf9823d33458239074a0d7ee638b247f1fa2c", "vout": 0, "nValue": 0.001}]' '{"XoRDiv9z12ECsYCNjtHjDvV1Nn4KSBa6xRfHT1c3nKY1CwDiz5rzSMZL7QCgvuF1T5Kq43o1fMqBxbWQ": 0.001, "QLsHc5DgnpMjPaDSuEF5gXt7ccgmLtgh2N": 0.0005}'`
TX=`elements-cli blindrawtransaction $TX`
TX=`elements-cli signrawtransaction $TX | jq -r '.hex'`
elements-cli sendrawtransaction $TX
```

### Limitations
The implementation of Confidential Transactions in Liquid has some important
limitations to be aware of. The CT implementation only hides a certain number of
the digits of the amount of each transaction output. The exact numeric limits
will be set once the production Liquid network is ready, but they will work as
follows: There will be a 'minimum confidential amount' that will be a round
number of BTC, probably around 0.0001 BTC. There will be a 'maximum confidential
amount' that will be 2<sup>32</sup> times the minimum amount, probably around
500,000 BTC.

Digits smaller than the minimum will be revealed to observers; for example, if
the minimum is 0.0001 BTC, a transaction output of 123.456789 BTC will look like
"?.????89 BTC". The tiny amount of information about the value leaked in this
way is unlikely to be important, but be aware that this could allow observers to
'follow' coins by linking subsequent transactions with identical amounts. All
values can be rounded to the minimum to avoid revealing information in this way
if preferred.

A transaction output larger than the maximum will reveal the order of magnitude
of the amount to observers, AND will reveal additional digits at the bottom of
the amount. (Technical details: The minimum amount will effectively be 'raised'
such that 2<sup>32</sup> times the new minimum is large enough to cover the
transaction.)

For example, if the maximum is 500k BTC, then all outputs under
that amount will look the same, but an output between 500k and 5M BTC will be
visible as such to observers (but not the exact amount within that range), and
will also reveal one additional digit of the low end of the amount. Revealing
the range in this way could be a very significant privacy leak; splitting such
extremely large transactions to keep them under the maximum confidential amount
is strongly recommended.

<div class="ui message">
  <h4 class="header">Want to learn more?</h4>
  <p>Gregory Maxwell's <a href="/elements/confidential-transactions/investigation.html">original investigation into Confidential Transactions</a> has the mathy details!</p>
</div>
