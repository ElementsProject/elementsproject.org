---
title: Signature Covers Value
description: This allows the signature on a transaction to be invalidated if the inputs have been spent, making it faster and easier to validate a transaction, simply by checking its signature.
image: /img/signature-covers-value.svg
source: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/elements/signature-covers-value/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/elements/signature-covers-value/index.md
---

*Principal Investigator: Glenn Willen*

The signatures verified by the CHECKSIG operators now cover the output value of spent inputs. This avoids the need for hardware signing devices to know the full previous transactions whose outputs are spent; if they are being lied to, the resulting signature is invalid anyway.

A side effect of this change is that signing now needs to know the values (blinded or not) consumed by the transaction’s inputs.
