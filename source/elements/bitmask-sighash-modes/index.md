---
title: Bitmask Sighash Modes
description: Allow arbitrary, miner-rewritable bitmasks of transaction inputs and outputs.
image: /img/bitmask-sighash-modes.svg
source: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/elements/bitmask-sighash-modes/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/elements/bitmask-sighash-modes/index.md
---

*Principal Investigator: Glenn Willen*
 * [feature-bitmasksighash](https://github.com/ElementsProject/elements/tree/feature_bitmasksighash) - EXAMPLE branch of Bitmask Sighash modes

The new CHECKSIG2 operator allows arbitrary, miner-rewritable bitmasks of inputs and outputs. This allows for more complex contractual pre-commitment schemes, such as signed offers with change in a distributed asset exchange.
