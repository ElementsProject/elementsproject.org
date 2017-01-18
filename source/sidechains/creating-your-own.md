---
title: Building A New Sidechain with Elements
edit: https://github.com/ElementsProject/elementsproject.github.io/blob/master/source/sidechains/creating-your-own.md
source: https://github.com/ElementsProject/elementsproject.github.io/edit/master/source/sidechains/creating-your-own.md
---

This is step-by-step guide will walk you through building your own sidechain and
setting up a simple single-signer peg with a `regtest`-powered mainchain.  This
configuration works to run a sidechain with a 1-of-1 functionary/blocksigner,
convenient for local development and testing.

There are several other ways of deriving consensus on a sidechain.  See [the
Deterministic Peg Element](/elements/deterministic-peg.html) for more details.

#### Prerequisites
You'll need a working version of Elements.  Follow [the Elements build
instructions](https://github.com/bitcoin/bitcoin/blob/master/doc/build-unix.md)
to get set up.

### Creating your own blockchain
Just like in Bitcoin, Elements can be started in `regtest` mode which allows to
easily create test chains and networks.

1. Start Elements:
  > `elementsd -regtest -daemon`
2. Create an alias for the RPC client:
  > `alias bc="elements-cli -regtest"`    
  <div class="ui info message">
    In Elements, blocks have to be signed by a quorum of the federation. However, just like in Bitcoin the conditions in regtest modes are not enforced, so you can simply create a block with `bc generate 1`.
  </div>
3. Create a chain where we predetermine who is allowed to sign blocks. We start with creating a fresh keypair.
  >     ADDR=`bc getnewaddress`
  >     PUBKEY=`bc validateaddress $ADDR | jq -r '.pubkey'`
  >     PRIVKEY=`bc dumpprivkey $ADDR`
4. Create a 1-of-1 multisig script to use as a block requirement.
  >     SIGNBLOCKSCRIPT=`bc createmultisig 1 \[\"$PUBKEY\"\] | jq -r '.redeemScript'`
5. Stop the daemon and create a new chain using the blocksigner script
  >     bc stop
  >     rm -rf ~/.bitcoin/elementsregtest
  >     elementsd -regtest -daemon -signblockscript=$SIGNBLOCKSCRIPT
  >     bc importprivkey $PRIVKEY
  >     NEW_BLOCK=`bc getnewblockhex`
  >     BLOCKSIG=`bc signblock $NEW_BLOCK`
    <div class="ui info message">
      If there were multiple blocksigners, you'd need to distribute `NEW_BLOCK`, collect signatures, then call `combineblocksigs`.  We'll leave this as an excercise to the reader.
    </div>
  >     SIGNED_BLOCK=`bc combineblocksigs $NEW_BLOCK \[\"$BLOCKSIG\"\] | jq -r '.hex'`
    * ensure that the output of combineblocksigs has "complete" true
  > `bc getblockcount`
    * check the current block count
  > `bc submitblock $SIGNED_BLOCK`
  > `bc getblockcount`
    * check that the chain advanced by one block

Block generation can be easily automated in a shell script.

#### Congratulations!
Your chain is online and already accessible, just let other nodes connect to you:
```
bc addnode <your_url>
```

### Moving Bitcoin into your Sidechain
You might have figured out that while you are in `regtest` mode you own all
coins on the elements chain. Of course, in production you first have to use a
mechanism known as peg-in to move coins from the main chain to the elements
sidechain. Let's set up our own sidechain federation to handle the peg.

1. Ensure that you have bitcoind 0.13.1 installed and elements as well as bitcoin are shut down.
2. Elements fully validates that peg-in transactions exists in Bitcoin. Therefore, it opens a RPC connection to bitcoind and checks that a particular block is in the chain and has the required confirmations. We need to ensure that the elements daemon is correctly talking to Bitcoin.
    * The configuration of Elements is getting larger, so we best create a config file in a new data directory.
    * `BETADATADIR=/tmp/elementsdatadir/`
    * `mkdir $BETADATADIR`
    * Put the following into $BETADATADIR/elements.conf
        ```
        rpcuser=bitcoinrpc
        rpcpassword=password
        rpcport=8339
        daemon=1
        discover=0
        testnet=0
        regtest=1

        mainchainrpchost=127.0.0.1
        mainchainrpcport=8338
        mainchainrpcuser=bitcoinrpc
        mainchainrpcpassword=password

        validatepegin=1
        txindex=1
        ```
    * Now do the same for bitcoin
    * `BITCOINDATADIR=/tmp/bitcoindatadir/`
    * `mkdir $BITCOINDATADIR`
    * put the following into $BITCOINDATADIR/bitcoin.conf
        ```
        rpcuser=bitcoinrpc
        rpcpassword=password
        rpcport=8338
        daemon=1
        discover=0
        testnet=0
        regtest=1
        txindex=1
        ```
* In the previous section we've used our own public key for the blocksigner script. We will use the same for the federation script. This is the script that owns the coins on the sidechain.
* Let's start bitcoin `bitcoind -datadir=$BITCOINDATADIR` and elements `elementsd -datadir=$BETADATADIR -signblockscript=$SIGNBLOCKSCRIPT -fedpegscript=$SIGNBLOCKSCRIPT`
* Let's update the elements-cli alias to use the new datadir
    * `alias bc="elements-cli -datadir=$BETADATADIR"`
    * `alias bitc="bitcoin-cli -datadir=$BITCOINDATADIR"`
* Create some coins on the main chain
    * `bitc generate 101`
* We can't create a regular peg-in yet, because there are no WPV outputs in regtest mode. We first create them by `sendtomainchain <addr>`. Note that peg-outs don't work, because you have no pegoutwatcher running.
* Now you can perform the regular peg-in steps, by first calling `getpeginaddress` on elements then sending coins with bitcoin, then -- again on elements -- claiming coins with `claimpegin`. Ensure that both chains are mining all the time.
