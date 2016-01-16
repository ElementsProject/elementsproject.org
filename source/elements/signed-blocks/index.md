---
title: Signed Blocks
description: Blocks can be cryptographically signed, allowing the creator of the block to verify their identity in the future.
image: /img/signed-blocks.svg
branch: block-signing-0.10
source: https://github.com/ElementsProject/elementsproject.github.io/blob/relaunch/source/elements/signed-blocks/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/relaunch/source/elements/signed-blocks/index.md
---

*Principal Investigator: Jorge Timón*

SHA256d proof of work is replaced with the system’s scripting system, just
signing blocks instead of transactions. In other words, the Dynamic Membership
Multi-party Signature (DMMS) is replaced with a (Static Membership) Multi-party
Signature. This has also been described in the past as ["private chains"][frei].

The Elements Alpha release uses a threshold of functionaries as a protocol
adaptor and also to sign blocks of transactions.  In a future release we plan to
replace the block-signing with merge-mining, though the functionaries remain to
communicate the transfer transactions to the main chain.   The Signed Blocks
feature serves to provide transaction processing functionality until
merge-mining is implemented.  Our intent is to later phase in the fully
decentralised 2-way peg mechanism to replace the functionaries. 

[frei]: http://freico.in/docs/freimarkets.pdf
