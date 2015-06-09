# Sidechain Elements
![Sidechain Elements logo](http://i.imgur.com/Vbhiqop.png)

Development project of Open source components and developer sidechains for advancing the art of Bitcoin.

PARAGRAPH SUMMARY OF THE GOALS OF ELEMENTS AND COLLABORATIVE DEVELOPMENT APPROACH

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

# Elements (feature advancement for Bitcoin)

## Elements contained in Alpha Sidechain
* item
* item

## Proposed Elements
 * [feature-assets](https://github.com/ElementsProject/bitcoin/tree/feature_assets) - branch of ongoing assets dev 
 * [feature-bitmasksighash](https://github.com/ElementsProject/bitcoin/tree/feature_bitmasksighash) - branch of Bitmask Sighash modes

#### Sidechain Elements Principal Investigators and Contributors
@apoelstra, @gmaxwell, @jtimon, @jwilkins, @pstratem, @sipa, @TheBlueMatt, @wtogami
