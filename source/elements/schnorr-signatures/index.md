---
title: Schnorr Signature Validation
description: A new way of constructing signatures for transactions, both improving efficiency of validating a transaction and offering new modes of multi-signature.
image: /img/confidential-transactions.svg
source: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/elements/schnorr-signatures/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/elements/schnorr-signatures/index.md
---

*Principal Investigator: Patrick Strateman*

Instead of DER-encoded ECDSA signatures over the secp256k1 curve, the CHECKSIG and related operators now use densely packed Schnorr signatures over the same curve. The advantages are:
* Efficient threshold signatures for n-of-n. Multiple Schnorr signatures can be combined to end up with a signature valid for the sum of the public keys, so arbitrarily large n-of-n multisig can be done by only communicating the single sum signature, which can be verified with a single CHECKSIG operation.
* Smaller signatures (64 bytes instead of 71-72) with none of the problems that DER encodings have caused for Bitcoin.
Potential support for batch validation (up to a factor 2 speedup to verify groups of 32 signatures at once). This requires knowing the R.y coordinate (ECDSA ignores this) and at the script level, guaranteeing that all signature verification failure results in script failure (i.e., all CHECKSIG operators behave like CHECKSIGVERIFY).
Stronger security proof.
* Provably no inherent signature malleability, while ECDSA has a known malleability, and lacks a proof that no other forms exist. Note that Witness Segregation already makes signature malleability not result in transaction malleability, however.
* Slightly faster to sign/verify than ECDSA.
