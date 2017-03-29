---
title: Asset Issuance
description: Create new assets on a sidechain, with optional confidentiality.
image: /img/asset-issuance.svg
branch: issuance-final
source: https://github.com/ElementsProject/elementsproject.github.io/blob/master/source/elements/asset-issuance/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/master/source/elements/asset-issuance/index.md
---

<div class="ui info message">
  <h4 class="header">Looking for the original investigation?</h4>
  <p>Read <a href="/elements/asset-issuance/investigation.html">Jorge Timon's original investigation</a> to learn about the origins of this Element.</p>
</div>

Users can issue their own confidential assets which represent fungible ownership
of the underlying asset type representing by the newly created units, which
could theoretically represent any asset including vouchers, coupons, currencies,
deposits, bonds, shares, etc. (subject to the respective jurisdiction’s
regulatory requirements).

These assets can optionally be "blinded", causing the data in the transactions
(including amount and asset type) to be cryptographically obfuscated in such a
way that only the participating parties can see.  Participants may choose to
reveal a "blinding key", which grants visibility into the transaction.

This opens the door for building trustless exchanges, options, and other
advanced smart contracts involving those arbitrary assets and a "hostcoin".

### Issuing Assets
Use the all-new `issueasset` RPC command.  Here, we're issuing 1000 new tokens,
and creating 200 "reissuance" tokens.
```
$ elements-cli issueasset 1000 200
> {
  "txid": "13a2357b0a51114fae92127f7afc74847acf07f87e1bb4849715d1c75dbc9a92",
  "vin": "0",
  "entropy": "4dcc890a6fc4f593c609ffaa295940acb244904c1439aa9cb9d8192440b41da4",
  "asset": "8854427e5ffcb0b837e85832b901b1135cc4ac766f537e2a7f07b71a76c5b9cf",
  "token": "ca270d5552e81d15e4f45e41ff2d9c7e456599a7678286b80f8b41cae179b26a"
}
```

It may be convenient to create a name for this asset using `addassetlabel`.  <strong>This label can be used in place of the ID for all asset-compatible RPC calls.</strong>

```
$ elements-cli addassetlabel 8854427e5ffcb0b837e85832b901b1135cc4ac766f537e2a7f07b71a76c5b9cf funcoin
$ elements-cli dumpassetlabels
> {
  "achievement": "aef740ae340f3abbb620699fc243021572c2e9d966f88f98ba26999ddaa54d34",
  "bitcoin": "09f663de96be771f50cab5ded00256ffe63773e2eaa9a604092951cc3d7c6621",
  "funcoin": "8854427e5ffcb0b837e85832b901b1135cc4ac766f537e2a7f07b71a76c5b9cf"
}
```

#### Re-issuance
Re-issuing an asset is effectively a provable inflation in the asset type.  To
do this, use `reissueasset`.  Let's issue 20 of our tokens:

```
elements-cli reissueasset 8854427e5ffcb0b837e85832b901b1135cc4ac766f537e2a7f07b71a76c5b9cf 20
{
  "txid": "6b20c853521346d5bda3fe9e006292260cf409054224f920f3abf6297aca8176",
  "vin": 1
}
  
$ elements-cli getwalletinfo
> {
  "walletversion": 130000,
  "balance": {
    "funcoin": 1020.00000000
  },
  "unconfirmed_balance": {
  },
  "immature_balance": {
  },
  "txcount": 1117,
  "keypoololdest": 1490389457,
  "keypoolsize": 100,
  "paytxfee": 0.00000000,
  "hdmasterkeyid": "f5ff0a90ac04830fde2f952cae9e076f9c2b4d39"
}
```

### How it works
All outputs are tagged with their asset identifier. Consensus rules are modified so that the total inputs and outputs are checked separately per asset.
A new transaction type is added for creating issued assets (asset definition transactions). Like coinbase transactions, asset definition transactions (the new transaction type) have a null input, but unlike coinbases, asset definition transactions have more inputs in addition to that first null input. This difference not only helps us distinguish between the two: it also guarantees a source of entropy for the asset id (which is the sha256d hash of the transaction). Within an asset definition transaction, any number of outputs with 0 as asset ID can be included with any amount and they will be treated as the initial unspent outputs for the newly created asset.

This technology is similar to colored coins in many ways, but explicit and consensus-enforced tagging has many advantages:

* Supports SPV wallets much more efficiently.
* Allows more complex consensus-enforced contracts.
* Benefits from other consensus-enforced extensions (ie confidential transactions would not be compatible with colored coins on top of Alpha).
* Opens the door for further consensus-enforced extensions that rely on the chain being able to operate with multiple assets.

Currently only the hostcoin can be used to pay fees, but it should be possible to pay fees of different asset types simultaneously.
In this first version all units of a given type must be issued within the asset definition transaction. In future versions it will be possible to define assets with a dynamic supply that can be increased after the definition, allowing the issuer to create new units.
Future versions can also implement consensus enforced interest that would be interesting for p2p lending and issuance of assets with built-in demurrage (negative interest) among other things.
