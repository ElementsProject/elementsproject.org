---
title: Deterministic Pegs
description: Deterministic Pegs allow cross-chain transactions to be constructed in a decentralized fashion.  Tokens can be moved from one blockchain to another.
image: /img/deterministic-pegs.svg
source: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/elements/deterministic-pegs/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/elements/deterministic-pegs/index.md
---

*Principal Investigator: Matt Corallo*

Deterministic pegs allow Elements Alpha to carry redeemable testnet coins without any modifications to testnet itself. Transfers into Alpha are validated by all full nodes, optionally with the assistance of an RPC call to a testnet node to validate blockchain membership without the presence of compressed SPV proofs in testnet. Transfers out of Alpha are performed by a federation of functionaries which are trusted to hold the coins for Alpha.

Sidechains, like other alternative chains, can also be secured by merge-mining.  However during a bootstrap period of introduction of a new chain, unless the start of merge mining were very well synchronised, there will be a period of lower hashrate. During the early stages of this bootstrap the chain could have low enough hashrate to present a security risk even against a modest powered attacker. Given the challenges of synchronising something as organic and decentralised by design as bitcoin mining, we therefore need a mechanism to bootstrap chain security.  We start in this release with a threshold of functionaries and are plan for a later version to phase in merge-mining.
