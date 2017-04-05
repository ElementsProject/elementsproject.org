---
title: Confidential Addresses
---

The most visible implication of Confidential Transactions is the introduction of
a new default address type, confidential addresses:

```
CTEwQjyErENrxo8dSQ6pq5atss7Ym9S7P6GGK4PiGAgQRgoh1iPUkLQ168Kqptfnwmpxr2Bf7ipQsagi
```

The most obvious differences are that it starts with ``CT`` and is longer than
usual. This is due to the inclusion of a public blinding key prepended to the
base address. In the Elements Wallet, the blinding key is derived by using the
wallet's master blinding key and unblinded P2PKH address. Therefore the receiver
alone can decrypt the sent amount, and can hand it to auditors if needed. On the
sender's side, ``sendtoaddress`` will use this pubkey to transmit the necessary
info to the receiver, encrypted, and inside the transaction itself. The sender's
wallet will also record the amount and hold this in the ``wallet.dat`` metadata
as well as the ``audit.log`` file.

```
$ elements-cli validateaddress CTEwQjyErENrxo8dSQ6pq5atss7Ym9S7P6GGK4PiGAgQRgoh1iPUkLQ168Kqptfnwmpxr2Bf7ipQsagi
> {
  "isvalid": true,
  "address": "CTEwQjyErENrxo8dSQ6pq5atss7Ym9S7P6GGK4PiGAgQRgoh1iPUkLQ168Kqptfnwmpxr2Bf7ipQsagi",
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

<div class="ui message">
  <h4 class="header">Did you know?</h4>
  <p>By sharing the blinding key used in the construction of a single confidential transaction, users can share access to the transaction's details.  <a href="/elements/confidential-transactions/selective-disclosure.html">Read more about selective disclosure &raquo;</a></p>
</div>