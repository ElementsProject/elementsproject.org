---
title: Liquid
source: https://github.com/ElementsProject/elementsproject.github.io/blob/relaunch/source/sidechains/liquid/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/relaunch/source/sidechains/liquid/index.md
data:
  elements: ct
---
Liquid is a commercial sidechain that combines [Confidential Transactions](/elements/confidential-transactions) and
several other Elements to provide high-speed transactions between Bitcoin
Exchanges.

Instead of proof of work (like in Bitcoin), Liquid depends on a distributed
group of "signatories", or functionaries, to create blocks.  These functionaries
are hardened black boxes that enforce the rules of the network as long as they
are connected to the Internet.  We have distributed these functionary boxes
across the world to a number of participants, known as "the functionary grid".

<img class="ui medium right floated image transition visible bordered" data-src="/sidechains/liquid/functionary-consensus.gif" src="/sidechains/liquid/functionary-consensus.gif" alt="Liquid Functionary Consensus" />

When it is time to append a new block to the Liquid sidechain, the block is
signed by the first functionary in the grid, then handed to the next.  Each time
the block is passed to the next functionary, it is checked by the code running
inside the black box to make sure it follows the rules, then is signed and
passed on to the next until a supermajority of nodes have signed the block.

Today, key players in the Bitcoin market, including exchanges, payment
processors, traders, and remitters, experience delays when moving bitcoin
between accounts in different locations. We refer to this as Interchange
Settlement Lag (ISL) – a host of liquidity inefficiencies including latency and
confirmation times that hinder the overall prospects of the Bitcoin ecosystem.
Dealing with these issues requires market participants to maintain multiple
balances and accounts across the market to avoid ISL, increasing overall capital
requirements and exposure to the possibility of counterparty risk.

Liquid is a powerful sidechain with wide-reaching implications.  To learn more,
[read the Liquid announcement](https://www.blockstream.com/2015/10/12/introducing-liquid/).

<a href="mailto:liquid@blockstream.com" class="ui button primary huge">Contact Blockstream To Learn More<i class="ui icon chevron right"></i></a>
<!-- <a href="https://blockstream.io" class="ui button primary huge">Read the Liquid Whitepaper<i class="ui icon chevron right"></i></a> -->
