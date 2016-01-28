---
title: Basic Asset Issuance
description: Create new assets on a sidechain by using Bitcoin as a bond.
image: /img/asset-issuance.svg
branch: multi-asset-0.11
source: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/elements/asset-issuance/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/elements/asset-issuance/index.md
---

*Principal Investigator: Jorge Timón*
 * [feature branch multi-asset-0.10](https://github.com/ElementsProject/elements/tree/multi-asset-0.10) - branch of ongoing assets dev

Users can issue their own assets which represent fungible ownership of the underlying asset type representing by the newly created units, which could theoretically represent any asset including vouchers, coupons, currencies, deposits, bonds, shares, etc (subject to the respective jurisdiction’s regulatory requirements.

This opens the door for building trustless exchanges, options, and other advanced smart contracts involving those arbitrary assets and the “hostcoin” (a native asset whose ID is equal to the hash of the genesis block or chain ID; in Alpha’s case, it is the federated-peg coin which is backed by testnet coins, see “Deterministic peg” section).

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
