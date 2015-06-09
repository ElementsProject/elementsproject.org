# Sidechain Elements
![Sidechain Elements logo](http://i.imgur.com/Vbhiqop.png)

Development project of Open source components and developer sidechains for advancing the art of Bitcoin.

Elements is a collection of experiments to bring more technical innovation to Bitcoin.

Our first release is Elements Alpha, a developer sidechain and network that introduces several new technologies on a sidechain, pegged to Bitcoin’s testnet. All code is open source, like Bitcoin itself, and others are encouraged to contribute to the project as it evolves.

Elements Alpha is intended to be a technology demo and testing environment. Not all features are ready yet (see Proposed Features), and the blockchain is intended to be short-lived and easily replaced as the technology evolves.

Elements Alpha functions as a sidechain to Bitcoin’s testnet, though the peg mechanism currently works through a centralized protocol adapter, as described in the Sidechains whitepaper in appendix A. It relies on an auditable federation of signers to manage the testnet coins transferred into the sidechain (see the Deterministic Peg feature) and to produce blocks (see the Signed Block feature). This makes it possible to immediately explore the new chain’s possibilities, using different security trade-offs. We plan to, in a later release, upgrade the protocol adapter to support merge-mining of the sidechain, and ultimately to phase in the full 2-way pegging  mechanism.

“It's nice working on something without millions of BTCs resting on it, and still have a path to production use.”

#### License and Disclaimer
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
# Elements (features under development)

## Elements currently in the alpha dev sidechain
* item
* item

## Proposed Elements
 * [feature-assets](https://github.com/ElementsProject/bitcoin/tree/feature_assets) - branch of ongoing assets dev 
 * [feature-bitmasksighash](https://github.com/ElementsProject/bitcoin/tree/feature_bitmasksighash) - branch of Bitmask Sighash modes

# How to try the Dev Sidechain?
#### Source Code
* https://github.com/ElementsProject/bitcoin - contains isolated feature and dev sidechains braches
 * [branch alpha](https://github.com/ElementsProject/bitcoin/tree/alpha) - testnet dev sidechain demo

#### Development Discussion
* https://lists.linuxfoundation.org/mailman/listinfo/sidechains-dev sidechains-dev discussion list

# Alpha Testnet Dev Sidechain
WRITE PARAGRAPH ABOUT IT HERE

#### Build Instructions
```
# https://github.com/bitcoin/bitcoin/tree/master/doc
# Please refer to the Bitcoin documentation to install the required build dependencies/
git clone https://github.com/ElementsProject/bitcoin
git checkout alpha
./autogen.sh
./configure
make
# If your build was successful, you will find src/alphad, src/alpha-cli and src/qt/alpha-qt 

```

The Data Directory of the alpha testnet dev sidechain lives within your existing Bitcoin [Data Directory](https://en.bitcoin.it/wiki/Data_directory).  For example, in Linux `~/.bitcoin/alphatestnet3` contains the Alpha blocks, indicies and wallet.

#### Moving coins between Testnet and Alpha
PARAGRAPH ABOUT PEG TRANSFER PROCESS HERE ... 

* [testnet-faucet](https://testnet-faucet.elementsproject.org/)
* [alpha-faucet](https://alpha-faucet.elementsproject.org/) - notice anything different about the addresses?

For your convenience, these faucets allow you to quickly obtain coins on either the testnet or alpha network without waiting for the customary confirmation and contest safety periods.

#### Sidechain Elements Principal Investigators and Contributors
@apoelstra, @gmaxwell, @jtimon, @jwilkins, @pstratem, @sipa, @TheBlueMatt, @wtogami
