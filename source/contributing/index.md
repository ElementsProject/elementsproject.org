## Contributing to the Elements Project
#### Source Code
* https://github.com/ElementsProject/elements - contains isolated feature and dev sidechains braches
 * [branch alpha](https://github.com/ElementsProject/bitcoin/tree/alpha) - testnet dev sidechain demo

#### Development Discussion
* Development Discussion List: [sidechains-dev list](https://lists.linuxfoundation.org/mailman/listinfo/sidechains-dev)
* Freenode IRC: #sidechains-dev [[webchat](http://webchat.freenode.net/?channels=%23sidechains-dev)]
* Bug Reports: Please submit issues to [github](https://github.com/ElementsProject/elements/issues).
* Pull Requests: Please submit pull requests to [github](https://github.com/ElementsProject/elements/pulls).


#### Build Instructions
```
# https://github.com/bitcoin/bitcoin/tree/master/doc
# Please refer to the Bitcoin documentation to install the required build dependencies/
git clone https://github.com/ElementsProject/elements
cd elements
git checkout alpha
./autogen.sh
./configure
make
# If your build was successful, you will find src/alphad, src/alpha-cli and src/qt/alpha-qt 

```

The Data Directory of the alpha testnet dev sidechain lives within your existing Bitcoin [Data Directory](https://en.bitcoin.it/wiki/Data_directory).  For example, in Linux `~/.bitcoin/alphatestnet3` contains the Alpha blocks, indicies and wallet.

#### Moving coins between Testnet and Alpha
See [alpha-README.md](https://github.com/ElementsProject/elements/blob/alpha/alpha-README.md) for instructions on how to transfer testnet coins to the alpha network and back.  Note that there is a lengthy confirmation and contest period that you must wait for a peg transfer to complete.

* [testnet-faucet](https://testnet-faucet.elementsproject.org/)
* [alpha-faucet](https://alpha-faucet.elementsproject.org/)

For your convenience, these faucets allow you to quickly obtain coins on either the testnet or alpha network without the lengthy wait for the confirmation and contest safety periods.

# FAQ
* **Is this an altcoin?**   No.  The key thing to understand about sidechains is value is transferred to/from the main chain.  No new coins are created and the total money supply remains constant.
* ADDME
