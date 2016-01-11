---
title: Relative Lock Time
description: Allows a transaction to be time-locked, preventing its use in a new transaction until a relative time change is achieved.
image: /img/time-lock.svg
source: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/elements/relative-lock-time/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/elements/relative-lock-time/index.md
---

*Principal Investigator: Mark Friedenbach*

The consensus-enforced semantics of the sequence number field is modified to enable a signed transaction input to remain invalid for a defined period of time after confirmation of its corresponding output, for the purpose of supporting consensus-enforced transaction replacement features.

Bitcoin has sequence number fields for each coin a transaction is spending. The original idea appears to have been that the highest sequence number should dominate and miners should prefer it over lower sequence numbers. This was never really implemented, and the half implemented code seemed to be making the assumption that miners would honestly prefer the higher sequence numbers, even if the lower ones were much more profitable. That turns out to be a dangerous assumption, and so most have assumed that kind of sequence number mediated replacement was useless because there was no way to enforce "honest" behaviour, as even a few rational (profit maximizing) miners would break that completely. This change provides the missing piece that makes sequence numbers do something with respect to enforcing transaction replacement without assuming anything other than profit-maximizing behaviour on the part of miners. A new opcode is added which enables Bitcoin scripts to check these constraints, CHECKSEQUENCEVERIFY.

Relative lock-times can be used for all the same purposes as regular (absolute) lock-times, such as time-locked escrow services, but the relative form is of particular interest in applications where the blockchain is used as a communication medium. For example, the contest period of the two-way peg is most naturally expressed as a relative lock-time condition beginning with the transaction announcing the proof of withdraw.
