---
title: Compiling the Alpha Sidechain Source Code
edit: https://github.com/ElementsProject/elementsproject.github.io/blob/relaunch/source/sidechains/alpha/building.md
source: https://github.com/ElementsProject/elementsproject.github.io/edit/relaunch/source/sidechains/alpha/building.md
---

## Build Instructions
If you've already forked [the Elements GitHub repository][elements-github],
getting started is easy.

<pre style="overflow: inherit;">
# https://github.com/bitcoin/bitcoin/tree/master/doc
# Please refer to the Bitcoin documentation to install the required build dependencies/
git clone https://github.com/ElementsProject/elements
cd elements
git checkout alpha
./autogen.sh
./configure
make
# If your build was successful, you will find src/alphad, src/alpha-cli and src/qt/alpha-qt
</pre>

The Data Directory of the alpha testnet dev sidechain lives within your existing Bitcoin [Data Directory](https://en.bitcoin.it/wiki/Data_directory).  For example, in Linux `~/.bitcoin/alphatestnet3` contains the Alpha blocks, indicies and wallet.

[elements-github]: https://github.com/ElementsProject/elements
