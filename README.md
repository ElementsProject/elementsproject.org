# Sidechain Elements
![Sidechain Elements logo](http://i.imgur.com/Vbhiqop.png)

Elements is an open source, collaborative project where we work on a collection of experiments to rapidly bring more technical innovation to Bitcoin.  Elements are features that are proposed and developed in this technical community that in arbitrary combinations can be fashioned into sidechains.

“It's nice working on something without millions of BTCs resting on it, and still have a path to production use.”

#### License
```
Permission is hereby granted, without written agreement and without
license or royalty fees, to use, copy, modify, and distribute this
software and its documentation for any purpose, provided that the
above copyright notice and the following two paragraphs appear in
all copies of this software.

IN NO EVENT SHALL THE COPYRIGHT HOLDER BE LIABLE TO ANY PARTY FOR
DIRECT, INDIRECT, SPECIAL, INCIDENTAL, OR CONSEQUENTIAL DAMAGES
ARISING OUT OF THE USE OF THIS SOFTWARE AND ITS DOCUMENTATION, EVEN
IF THE COPYRIGHT HOLDER HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH
DAMAGE.

THE COPYRIGHT HOLDER SPECIFICALLY DISCLAIMS ANY WARRANTIES, INCLUDING,
BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND
FITNESS FOR A PARTICULAR PURPOSE.  THE SOFTWARE PROVIDED HEREUNDER IS
ON AN "AS IS" BASIS, AND THE COPYRIGHT HOLDER HAS NO OBLIGATION TO
PROVIDE MAINTENANCE, SUPPORT, UPDATES, ENHANCEMENTS, OR MODIFICATIONS.
```
# Elements: features under investigation

## Current Elements
###Confidential Transactions 
*Principal Investigator: Greg Maxwell* [[*Peer reviewed technical details*](https://people.xiph.org/~greg/confidential_values.txt)]

One of the most powerful new features being explored in Elements is Confidential Transactions. This keeps the amounts transferred visible only to participants in the transaction (and those they designate), while still guaranteeing that no more coins can be spent than are available in a cryptographic way.

This goes a step beyond the usual privacy offered by Bitcoin’s blockchain, which relies purely on pseudonymous - but public - identities. This matters, because insufficient financial privacy can have serious security and privacy implications for both commercial and personal transactions. Without adequate protection, thieves and scammers can focus their efforts on known high-value targets, competitors can learn business details, and negotiating positions can be undermined. 

The most visible implication of Confidential Transactions is the introduction of a new address type (confidential addresses). These are longer than usual as they also includes a blinding key for the values. They are the default address type in Alpha.

* ADDME

## Proposed Elements
 * [feature-assets](https://github.com/ElementsProject/elements/tree/feature_assets) - EXAMPLE branch of ongoing assets dev 
 * [feature-bitmasksighash](https://github.com/ElementsProject/elements/tree/feature_bitmasksighash) - EXAMPLE branch of Bitmask Sighash modes

# Testnet Dev Sidechain Demo: Elements Alpha
To make it easy for the community to test the latest Elements, this project combines the best of them into dev sidechains.  The first release is Elements Alpha, a developer sidechain and network that introduces several new technologies on a sidechain, pegged to Bitcoin’s testnet. All code is open source, like Bitcoin itself, and others are encouraged to contribute to the project as we work to improve and add additional Elements.  Elements Alpha is intended to be a technology demo and testing environment.  Proposed Elements were not ready, and as a testnet development sidechain, this blockchain is intended to be short-lived and easily replaced as the technology evolves.

Elements Alpha functions as a sidechain to Bitcoin’s testnet, though the peg mechanism currently works through a centralized protocol adapter, as described in the Sidechains whitepaper in appendix A. It relies on an auditable federation of signers to manage the testnet coins transferred into the sidechain (see the Deterministic Peg feature) and to produce blocks (see the Signed Block feature). This makes it possible to immediately explore the new chain’s possibilities, using different security trade-offs. We plan to, in a later release, upgrade the protocol adapter to support fully decentralized merge-mining of the sidechain, and ultimately to phase in the full 2-way pegging  mechanism.

#### Source Code
* https://github.com/ElementsProject/elements - contains isolated feature and dev sidechains braches
 * [branch alpha](https://github.com/ElementsProject/bitcoin/tree/alpha) - testnet dev sidechain demo

#### Development Discussion
* Development Discussion List: https://lists.linuxfoundation.org/mailman/listinfo/sidechains-dev
* Freenode IRC #sidechains-dev [[webchat](http://webchat.freenode.net/?channels=%23sidechains-dev)]
* Bug Reports: Please submit issues to [github](https://github.com/ElementsProject/elements/issues).
* Pull Requests: Please submit pull requests [github](https://github.com/ElementsProject/elements/pulls).

#### Build Instructions
```
# https://github.com/bitcoin/bitcoin/tree/master/doc
# Please refer to the Bitcoin documentation to install the required build dependencies/
git clone https://github.com/ElementsProject/elements
git checkout alpha
./autogen.sh
./configure
make
# If your build was successful, you will find src/alphad, src/alpha-cli and src/qt/alpha-qt 

```

The Data Directory of the alpha testnet dev sidechain lives within your existing Bitcoin [Data Directory](https://en.bitcoin.it/wiki/Data_directory).  For example, in Linux `~/.bitcoin/alphatestnet3` contains the Alpha blocks, indicies and wallet.

#### Moving coins between Testnet and Alpha
FIXME: PARAGRAPH ABOUT PEG TRANSFER PROCESS HERE ... 

* [testnet-faucet](https://testnet-faucet.elementsproject.org/)
* [alpha-faucet](https://alpha-faucet.elementsproject.org/)

For your convenience, these faucets allow you to quickly obtain coins on either the testnet or alpha network without the lengthy wait for the confirmation and contest safety periods.

# FAQ
* _Is this an altcoin?_  No.  The key thing to understand about sidechains is value is transferred to/from the main chain.  No coins are created elsewhere.
* ADDME

#### Sidechain Elements Principal Investigators and Contributors
@apoelstra, @gmaxwell, @gwillen, @jonasschnelli, @jtimon, @jwilkins, @kanzure, @Luke-Jr, @maaku, @petertodd, @pstratem, @sipa, @TheBlueMatt, @wtogami
