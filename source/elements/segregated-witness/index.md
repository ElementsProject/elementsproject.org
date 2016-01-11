---
title: Segregated Witness
description: Reduce the required space for transactions in a block by a factor of 4.
image: /img/segregated-witness.svg
source: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/elements/segregated-witness/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/elements/segregated-witness/index.md
---

*Principal Investigator: Pieter Wuille*

With Segregated Witness, the specification of a transaction’s effects on the
ledger is separated from the data necessary to prove its validity (called a
witness in cryptography). This completely eliminates all known forms of
transaction malleability, and allows significant blockchain pruning
optimizations.

In Bitcoin, transactions contain both information about the effect on the ledger
(UTXOs being spent, addresses, and amounts involved) and data proving that the
transaction is authorized (input signatures). For Witness Segregation,
transaction IDs are redefined to only depend on the effect information, and
blocks commit separately to the witness data. This has several advantages:

* Bitcoin has seen some “Normalized Transaction ID” proposals, but these are effectively subsumed by Segregated Witness, which is both more efficient and more usable, as Normalized Transaction ID mechanisms still require rewriting dependent transactions after inputs are malleated. Such normalization is a necessary building block for higher-layer protocols such as Lightning.
* As transaction IDs no longer cover the signatures, they remove all forms of transaction malleability, in a much more fundamental way than BIP62 aims to do. This results in a larger class of multi-clause contract constructs that become safe to use.
* Potential for more efficient SPV output creation proofs (used by lightweight clients), as the signatures can be omitted from the transaction data without breaking the Merkle tree structure.
Potential for nodes that do not wish to store or verify old transaction signatures, to remove the witness data from disk or not transfer it at all even, reducing blockchain storage/bandwidth amounts by a large factor. In Alpha, the witness data size is even more significant than in Bitcoin, as it also includes large range proofs for the output values.
