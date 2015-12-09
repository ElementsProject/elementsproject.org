---
title: Announcing Sidechain Elements: Open source code and developer sidechains for advancing Bitcoin
source:
github: 
---
We're excited to announce the release of Sidechain Elements. Sidechains extend
Bitcoin functionality through interoperable blockchain networks and today's open
source release includes an
experime[![elements_logo](https://www.blockstream.com/wp-content/uploads/2015/06/elements_logo-300x78.png)](https://www.blockstream.com/wp-content/uploads/2015/06/elements_logo.png)ntal
sidechain that has a number of new working capabilities. With the release of
Sidechain Elements, Blockstream is moving this effort into the community. We're
inviting developers to work with us, to test and use the code for their
projects, and to share their proposals and code for additional capabilities.

Sidechains are decentralized, peer-to-peer networks that provide useful
security, risk, and performance enhancements for global systems of value
exchange that don't need intermediaries, central banks or other third parties.
They are distributed ledgers that are interoperable with each other and with
Bitcoin, leveraging the most secure blockchain and code infrastructure in an
additive way. Sidechains enable innovators to safely develop new applications
without jeopardizing Bitcoin's core code and putting billions of dollars worth
of digital currency at risk.

We began our work on sidechains almost one year ago first through extensive
discussions and debate with others in the technical community, and then in the
publication of a
[whitepaper](https://www.blockstream.com/2014/10/23/why-we-are-co-founders-of-blockstream/
"Why we co-founded Blockstream") and [launch of
Blockstream](https://www.blockstream.com/2014/11/17/blockstream-closes-21m-seed-round/
"Blockstream closes $21M seed round"). Over the past several months, we've been
coding and testing initial implementations all in preparation for today's
release.

Sidechain Elements consists of several components: the core network software to
build an initial testing sidechain, eight new features not currently supported
by Bitcoin, a basic wallet, and the code for moving coins between blockchains.
We've selected a collection of elements chosen to be both exciting and useful to
three audiences with overlapping interests: the broader Bitcoin community; core
technologists and smart-contract programmers; and businesses just starting to
explore blockchain use cases. The new elements include Confidential
Transactions, Basic Asset Issuance, Relative Lock Time and several others. We've
posted a video of our CTO, Greg Maxwell, walking through all of new
capabilities.

The initial sidechain included in Sidechain Elements works on a federated
security model; while it's still peer-to-peer and consensus-based, security for
the blockchain is provided by a set of predefined functionaries in an
arrangement called a Fed-Peg. A number of academic groups and individual
contributors have agreed to run the Sidechain Elements Fed-Peg, including
blockchain groups at Stanford, MIT, and Princeton. The sidechain does not
include mining or proof-of-work at this point.

In the coming weeks, we'll be publishing an early draft of a proposal for a
fully decentralized, two-way peg and merge-mined sidechains, which will enable
us to test other types of sidechain functionality.

Sidechains are an emerging technology, and this work is in its early stages. The
code and working sidechain provide a basis for research and prototyping. We'll
undertake many of these efforts, and anticipate many others will happen
independent of Blockstream with over 30 major financial institutions launching
blockchain innovation projects, as well as interest in this tech from other
Bitcoin and blockchain-based ventures.

**Here be dragons:** While much of the underlying science isn't new, this is an
alpha code release. We've intentionally focused on a Testnet sidechain and
strongly urge others to avoid implementations that involve bitcoin or other
real-world assets. Fiduciary code like this requires significant peer review
before moving onto production environments.

Sidechain Elements is available under the MIT open source license, along with
initial documentation, on Blockstream's code repo. We'll make ourselves
available to work with developers, and we invite the technical community to join
the discussion and get involved in moving sidechains and distributed ledger
technology forward. Complete info and links can be found on our new
[Developers](https://blockstream.com/developers/) page.
