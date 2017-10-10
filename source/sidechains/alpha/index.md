---
title: Elements Alpha
edit: https://github.com/ElementsProject/elementsproject.github.io/blob/master/source/sidechains/alpha/index.md
source: https://github.com/ElementsProject/elementsproject.github.io/edit/master/source/sidechains/alpha/index.md
---

**These instructions are outdated, and will eventually be removed. Elements Alpha does not support recent elements features, or receive backported security fixes. We recommend all new elements applications to be developed using `regtest` mode, and have provided instructions for setting up such test networks using recent builds of elements [here](https://github.com/ElementsProject/elements).**

To make it easy for the community to test [the latest
Elements][latest-elements], they are deployed on a public sidechain (pegged to
Bitcoin's `testnet`), <strong>Elements Alpha</strong>.  All code is open source,
like Bitcoin itself, and others are encouraged to contribute to the project as
we work to improve and add additional Elements.  Elements Alpha is intended to
be a technology demo and testing environment, but the same tools and practices
used to interact with it will integrate with production networks.

<div class="ui right huge fluid buttons">
<a href="/sidechains/creating-your-own.html" class="ui huge button">Build my own sidechain.</a>
<div class="or"></div>
<a href="/sidechains/alpha/getting-started.html" class="ui huge button primary">Join the Alpha Sidechain<i class="icon chevron right"></i></a>
</div>

<div style="clear: both;"></div>

<div class="ui message">
  <h4 class="header">Compiling</h4>
  <p>Just trying to run an Alpha node to build your prototype?  Jump straight to the
instructions.</p>
<a href="/sidechains/alpha/building.html" class="ui button fluid floated primary">Compiling Alpha from Source<i class="icon chevron right"></i></a>
</div>

<div style="clear: both;"></div>

### Introduction

Elements Alpha functions as a sidechain to Bitcoin’s `testnet`, though the peg
mechanism currently works through a centralized protocol adapter, as described
in [the Sidechains whitepaper][whitepaper]. It relies on an auditable federation
of signers to manage the testnet coins transferred into the sidechain via [the
"Deterministic Pegs" Element][deterministic-peg], and to produce blocks via [the
"Signed Blocks" Element][signed-blocks]. This makes it possible to immediately
explore the new chain’s possibilities, using different security trade-offs. We
plan to, in a later release, upgrade the protocol adapter to support fully
decentralized merge-mining of the sidechain, and ultimately to phase in the full
2-way peg mechanism.

#### Moving coins between Testnet and Alpha
See [alpha-README.md](https://github.com/ElementsProject/elements/blob/alpha/alpha-README.md) for instructions on how to transfer testnet coins to the alpha network and back.  Note that there is a lengthy confirmation and contest period that you must wait for a peg transfer to complete.

* [testnet-faucet](https://testnet-faucet.elementsproject.org/)
* [alpha-faucet](https://alpha-faucet.elementsproject.org/)

For your convenience, these faucets allow you to quickly obtain coins on either the testnet or alpha network without the lengthy wait for the confirmation and contest safety periods.

# FAQ
* **Is this an altcoin?**   No.  The key thing to understand about sidechains is value is transferred to/from the main chain.  No new coins are created and the total money supply remains constant.

[elements-github]: https://github.com/ElementsProject/elements
[compiling]: /sidechains/alpha/compiling.html
[latest-elements]: /elements#latest
[whitepaper]: https://blockstream.com/sidechains.pdf
[deterministic-peg]: /elements/deterministic-pegs
[signed-blocks]: /elements/signed-blocks
