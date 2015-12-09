---
title: The Alpha Sidechain
edit: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/sidechains/alpha/index.md
source: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/sidechains/alpha/index.md
---

To make it easy for the community to test the latest Elements, this project
combines the best of them into dev sidechains.  The first release is Elements
Alpha, a developer sidechain and network that introduces several new
technologies on a sidechain, pegged to Bitcoin’s testnet. All code is open
source, like Bitcoin itself, and others are encouraged to contribute to the
project as we work to improve and add additional Elements.  Elements Alpha is
intended to be a technology demo and testing environment.  Proposed Elements
were not ready, and as a testnet development sidechain, this blockchain is
intended to be short-lived and easily replaced as the technology evolves.

Elements Alpha functions as a sidechain to Bitcoin’s testnet, though the peg
mechanism currently works through a centralized protocol adapter, as described
in the Sidechains whitepaper in appendix A. It relies on an auditable federation
of signers to manage the testnet coins transferred into the sidechain (see the
Deterministic Peg feature) and to produce blocks (see the Signed Block feature).
This makes it possible to immediately explore the new chain’s possibilities,
using different security trade-offs. We plan to, in a later release, upgrade the
protocol adapter to support fully decentralized merge-mining of the sidechain,
and ultimately to phase in the full 2-way pegging  mechanism.

<a href="#" class="ui button huge primary">Browse the `alpha` Source on GitHub<i class="icon chevron right"></i></a>
