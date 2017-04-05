---
title: Using Confidential Transactions for Selective Disclosure
---

The [Confidential Transactions][confidential-transactions] element offers cryptographic privacy over the amounts of an asset used in
transactions on a sidechain.  There are many use cases for selectively disclosure some parts of
a transaction, for example to an auditor.

### The Blinding Key
The "Blinding Key" is a shared value between the participants that grants them
access to the cryptographically-concealed amount.  By sharing this key (out of
band), external parties will have the ability to "decrypt" the transaction.

In order to execute a third-party audit of transaction amounts, the blinding key
can be exported by the receiver and passed on to the auditor.

#### Retrieving the Blinding Key for a Particular Address
```
$ elements-cli dumpblindingkey CTEwQjyErENrxo8dSQ6pq5atss7Ym9S7P6GGK4PiGAgQRgoh1iPUkLQ168Kqptfnwmpxr2Bf7ipQsagi
> 5fd02f714d52b68bbbfef3b8e6d83be646fad1de5150e83d26a28496e00a2146
```

An auditor may then import the address and blinding key with
``importblindingkey`` to observe watch-only amounts.

```
$ elements-cli importaddress CTEwQjyErENrxo8dSQ6pq5atss7Ym9S7P6GGK4PiGAgQRgoh1iPUkLQ168Kqptfnwmpxr2Bf7ipQsagi
$ elements-cli listtransactions "*" 1 0 true
> []
  
$ elements-cli importblindingkey CTEwQjyErENrxo8dSQ6pq5atss7Ym9S7P6GGK4PiGAgQRgoh1iPUkLQ168Kqptfnwmpxr2Bf7ipQsagi 5fd02f714d52b68bbbfef3b8e6d83be646fad1de5150e83d26a28496e00a2146
$ elements-cli listtransactions "*" 1 0 true
> [
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

You may also inspect an address in full:
```
$ elements-cli validateaddress CTEwQjyErENrxo8dSQ6pq5atss7Ym9S7P6GGK4PiGAgQRgoh1iPUkLQ168Kqptfnwmpxr2Bf7ipQsagi
> {
  "isvalid": true,
  "address": "CTEwQjyErENrxo8dSQ6pq5atss7Ym9S7P6GGK4PiGAgQRgoh1iPUkLQ168Kqptfnwmpxr2Bf7ipQsagi",
  "scriptPubKey": "76a91405d5c237c5f2d90cfa22a22b75a1d1c1ede021a088ac",
  "confidential_key": "03b0f93d729839d3d96bfd7e20f11c7c6ae2016644d0d4cded6332dbfb61ed9067",
  "unconfidential": "2dZxbqgzXvANyj9SmyRR9LX3R2k8hg4iUWa",
  "ismine": true,
  "iswatchonly": false,
  "isscript": false,
  "pubkey": "031f17ad1acce63acf2d04cc59cb24423ab30f9345dd17476fd2380b02f878295d",
  "iscompressed": true,
  "account": "",
  "hdkeypath": "m/0'/0'/10'",
  "hdmasterkeyid": "f5ff0a90ac04830fde2f952cae9e076f9c2b4d39"
}

```
  
[confidential-transactions]: /elements/confidential-transactions

