---
title: The Alpha Sidechain
edit: https://github.com/ElementsProject/elementsproject.github.io/blob/master/source/sidechains/alpha/index.md
source: https://github.com/ElementsProject/elementsproject.github.io/edit/master/source/sidechains/alpha/index.md
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

<a href="/sidechains/alpha/getting-started.html" class="ui button huge right floated primary">Getting Started with the Alpha Sidechain<i class="icon chevron right"></i></a>

<div style="clear: both;"></div>

#### Compiling
Just trying to run an Alpha node to build your prototype?  Jump straight to the
instructions.

<<<<<<< HEAD
<a href="/sidechains/alpha/building.html" class="ui button fluid floated primary">Compiling Alpha from Source<i class="icon chevron right"></i></a>
=======
<a href="/sidechains/alpha/compiling.html" class="ui button fluid floated primary">Compiling Alpha from Source<i class="icon chevron right"></i></a>
>>>>>>> creating-sidechains

<div style="clear: both;"></div>

#### Moving coins between Testnet and Alpha
See [alpha-README.md](https://github.com/ElementsProject/elements/blob/alpha/alpha-README.md) for instructions on how to transfer testnet coins to the alpha network and back.  Note that there is a lengthy confirmation and contest period that you must wait for a peg transfer to complete.

* [testnet-faucet](https://testnet-faucet.elementsproject.org/)
* [alpha-faucet](https://alpha-faucet.elementsproject.org/)

For your convenience, these faucets allow you to quickly obtain coins on either the testnet or alpha network without the lengthy wait for the confirmation and contest safety periods.

# FAQ
* **Is this an altcoin?**   No.  The key thing to understand about sidechains is value is transferred to/from the main chain.  No new coins are created and the total money supply remains constant.

[elements-github]: https://github.com/ElementsProject/elements
[compiling]: /sidechains/alpha/compiling.html
