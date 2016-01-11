---
title: New Opcodes
description: Introduces DETERMINISTICRANDOM and CHECKSIGFROMSTACK, in addition to re-enabling several scripts previously enabled in Bitcoin.
image: /img/new-opcodes.svg
source: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/elements/opcodes/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/elements/opcodes/index.md
---

*Principal Investigator: Patrick Strateman*

Alpha enables several new script opcodes, in addition to the ones already supported by Bitcoin.
* Disabled opcodes. Bitcoin used to support a wider range of Script opcodes than exist now. Many were disabled for security reasons in 2010, and require a hard fork to re-enable them. Some of them had significant risks (unbounded memory usage), but not all of them. Alpha reintroduces these safe but disabled opcodes. They include string concatenation and substrings, integer shifts, and several bitwise operations.
* A new DETERMINISTICRANDOM operation which produces a random number within a range from a seed.
* A new CHECKSIGFROMSTACK operation which verifies a signature against a message on the stack, rather than the spending transaction itself.

These new opcodes have several use cases, including double-spent protection bonds, lotteries, merkle tree constructions to allow 1-of-N multisig with huge N (thousands), and probabilistic payments.
