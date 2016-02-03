# Getting Started With Sidechains
You might have heard of Sidechains by now – a way to test new blockchain ideas,
while still being protected the security of the Bitcoin mining network.
Blockstream has been hard at work [turning this idea into a reality][presentation],
and recently they released [the Elements Project][elements], which puts a huge
list of powerful new tools into the hands of developers.

So what's the first thing we're going to do?  Start playing with it, of course.

## Compiling
You're going to need to grab a few dependencies before you can compile.  If
you've already compiled Bitcoin before (a process I recommend everyone go
through), you probably have most of the required components – you can [skip
ahead to compiling Elements itself](#building-elements).  For others, I'm going
to start with one of the most common developer setups, a modern Linux
distribution (Ubuntu in our case) and compiling everything from scratch.

#### Getting the Compiler
Let's go ahead and get our basics complete.  For now, that starts with getting
a compiler and all the build tools.  In Ubuntu, this is provided by the
`build-essential` package:

```bash
sudo apt-get install build-essential
```

We're also going to want a few extra tools, perhaps most notably `autoconf`:

```bash
sudo apt-get install libtool autotools-dev autoconf pkg-config
```

#### Installing Dependencies
Bitcoin and Elements also require a list of dependencies you'll need installed
before you're able to compile, including `libssl`, `libboost`, and a number of
other `libboost-*` packages:

_**Important!** Make sure to use `libdb4.8`, **not** `libdb5.1` or later!  These
packages break certain functionality in Bitcoin and will not be conducive to a
successful build!_

```bash
sudo apt-get install libssl-dev libboost-all-dev libdb4.8-dev libdb4.8++-dev
```

_**Note:** `libboost-all-dev` is available on Ubuntu, but might not be so
convenient on other distributions.  Your mileage may vary – try compiling and
simply installing the packages the compiler claims are missing._

<a name="building-elements"></a>
## Building Elements
We're ready to download and compile the main body of work that comprises
Elements.  Like any other compiled package, we'll first acquire the source code,
then configure it for our environment, and finally compile it into some
executable binaries.

_**Note:** personally, I prefer keeping everything in a distinct project folder.
 To do this, I execute this first: `mkdir sidechains && cd sidechains` – you'll
likely be better organized in the long run if you start this way!_

Download the code via Git:
```bash
git clone https://github.com/ElementsProject/elements && cd elements
```

If you'd like, you can even fork the above repository on GitHub, and replace the
git URL with your personal one.  This is generally my approach.

You're now in the `elements` directory.  Let's compile `bitcoin` itself, which
is a necessary component for any sidechain:
```bash
git checkout mainchain
./autogen.sh && ./configure && make
mv src/bitcoin{d,-cli,-tx} ../
```

Give it a little while to configure and compile – this can take a significant
amount of time, depending on the speed of your computer.  Once complete (so long
as there are no errors), you should be able to execute `ls ..` and see three
binaries – `bitcoind`, `bitcoin-cli`, and `bitcoin-tx`.  You're ready to move
forward.

Let's checkout the `alpha` branch, which contains Blockstream's proposed
improvements to Bitcoin to implement sidechains, and complete the same process:
```bash
git checkout alpha
./autogen.sh && ./configure && make
mv src/alpha{d,-cli,-tx} ../
```

Again, provided there are no errors, `ls ..` should now include three additional
binaries: `alphad`, `alpha-cli`, and `alpha-tx` – these are the
Elements-specific binaries that implement sidechains, and expect to be able to
connect directly to the `bitcoind` instance you compiled earlier.

Let's fire these babies up.

## Running Elements
Now that we have working binaries for both Bitcoin and Elements, we can start
running them as nodes.  We'll be joining them to `testnet3`, the latest testnet
on the Bitcoin network.

You'll have to run two different binaries at once here - I'll leave that as an
exercise to the reader to manage, if I only insist that `tmux` provides a
wonderful split-screen capability within a single terminal!

Firstly, it'll help to alias some variables to configure the authentication for
the RPC communication between the Elements and Bitcoin binaries:

```bash
RPC_USER=user
RPC_PASS=pass
```

In screen one, let's get our Bitcoin daemon started:
```bash
./bitcoind -rpcuser=$RPC_USER -rpcpassword=$RPC_PASS -testnet -txindex
```

Since this will be the first time we've started our Bitcoin client, it will take
some time to synchronize (generally 2-3 hours).  Let's go ahead and fire up the
Elements binary before we go grab some coffee, though – again, very similar to
before, but this time with the `alphad` binary:

```bash
./alphad -rpcuser=$RPC_USER -rpcpassword=$RPC_PASS -testnet -rpcconnect=127.0.0.1 -rpcconnectport=18332 -tracksidechain=all -txindex -blindtrust=true
```

You'll notice some additional parameters, including `-tracksidechain` and
`-blindtrust`, but also some RPC parameters specifying where it can find a
"trustworthy" Bitcoin node.  In this case, we're supply our own node, which we
have compiled ourselves and know to be valid.

When both clients complete their synchronization, you're now a fully functional Elements/Bitcoin pair on the `testnet3` network!  Now's your chance to go grab
a coffee while we wait for that to complete.

## Moving Money
Hopefully you've given both Elements and Bitcoin enough time to sync by now.
The next natural step is to try moving some money into the network – to do this,
we'll need some `testnet3` Bitcoin to spend into the sidechain to acquire our
sidechain's tokens, and then we can spend those sidechain tokens to re-acquire
our Bitcoin.

### Compiling Tools
As this is intended as a developer preview, we don't have fancy interfaces for
moving money around – we'll need to build a few for ourselves.

Up first is the `secp256k1` library, which exposes all of the standard k1 curve
functionality:
```bash
git clone https://github.com/bitcoin/secp256k1
cd secp256k1
./autogen.sh && ./configure --with-bignum=no && make
make DESTDIR=`pwd`/install install
cd ..
```

The only notable component here is that we're using `make install` with a target
directory – we'll use this now for static linking in `contracthashtool`:
```bash
git clone https://github.com/blockstream/contracthashtool
cd contracthashtool
make CXXFLAGS="-I../secp256k1/install/usr/local/include -L../secp256k1/install/usr/local/lib -static"
cd ..
```

One last tool and we're almost ready – let's get a copy of Jeff Garzik's RPC
client:
```bash
git clone https://github.com/jgarzik/python-bitcoinrpc
```

Now, we're ready to move money.

### Magic
Let's generate a new sidechain wallet to store the tokens we're about to create
when we commit our testnet Bitcoin.  Go ahead and run `cd elements` to get into
the appropriate folder.

#### Funding Your Wallet
Since we just installed Bitcoin for the first time above, we probably don't have
any `testnet3` bitcoin.  Blockstream has [their own testnet faucet][testnet
faucet] for this purpose; let's get our Bitcoin address and request some funds:
```bash
../bitcoin-cli -testnet -rpcuser=user -rpcpassword=pass getnewaddress
```
You'll get an output of an address – make sure it starts with an `m`, which
designates a testnet address–and plug that into [the `testnet3` bitcoin faucet
][testnet faucet] to request some coins.

_**Note:** If you set a custom RPCUSER and RPCPASS in the earlier step, you'll
need to edit `./contrib/sidechain-manipulation.py` now to reflect those values somewhere
around lines 9 and 10._
```bash
./contrib/sidechain-manipulation.py generate-one-of-one-multisig sidechain-wallet
```

You'll see something like this as an output:

```bash
One-of-one address: 22E8QKHaTijFemPDwKvAk9qoTgagPfp8nBQiry87MMU1h2gQa8puPqVNtbNCN61ZUzfy1wDuXM1hS6o82
P2SH address: 2NFEWvrCjPGFQn6smEAUA8ehVr46PrCc8C5
```

Let's copy that P2SH address and use it to send some money:

```bash
./contrib/sidechain-manipulation.py send-to-sidechain 2NFEWvrCjPGFQn6smEAUA8ehVr46PrCc8C5 1
```
Don't forget to replace the address with the one you generated above, and to
supply the amount you're sending.  You should see an output something like this:
```bash
Sending 1 to 2NFEWvrCjPGFQn6smEAUA8ehVr46PrCc8C5...
(nonce: 94ffbf32c1f1c0d3089b27c98fd991d5)
Sent tx with id bf01b88710b6023125379510ebd84b373bee88217c80739a1144e5e92b4ee2d0
```
Take note of both the `nonce` and the transaction ID.  We'll need them to stake
our claim to the corresponding sidechain tokens in a moment.

Now, due to the nature of this sidechain implementation, you'll need to wait 10
blocks on the testnet blockchain for this transaction to be redeemable in the
sidechain.  This amounts to around 1.5 hours on `mainnet`, but shouldn't take
nearly this long on `testnet`.

Once completed, let's go ahead and claim – don't forget to replace the `nonce`
and transaction ID values, in that order:

```bash
./contrib/sidechain-manipulation.py claim-on-sidechain 2NCs5ufweTL8VHKNT6wrZMTkrnnmpZCy99j 94ffbf32c1f1c0d3089b27c98fd991d5 bf01b88710b6023125379510ebd84b373bee88217c80739a1144e5e92b4ee2d0
```

Again, the output will look something like this:
```bash
Redeeming from utxo 0377d218c36f5ee90244e660c387002296f3e4d5cac8fac8530b07e4d3241ccf:0 (value 21000000, refund 20999999)
Success!
Resulting txid: eabe26aba6286e1ee439baedeb75094ec0bcdaf54ed9481d9d2183e8a6424755
```

You've now got a spendable transaction on your sidechain!  Well, it'll be
redeemable in 144 sidechain blocks to make sure any outstanding forks are
resolved, but we've just claimed our first tokens in the sidechain.

We can now spend it using our 1-of-1 address from earlier:
```bash
./contrib/sidechain-manipulation.py spend-from-claim eabe26aba6286e1ee439baedeb75094ec0bcdaf54ed9481d9d2183e8a6424755 22E8QKHaTijFemPDwKvAk9qoTgagPfp8nBQiry87MMU1h2gQa8puPqVNtbNCN61ZUzfy1wDuXM1hS6o82
  Submitting tx to mempool...
  Success!
```

## What's Going On Here?
In this initial release of Elements, we've implemented something called
"federated peg".  Since the main Bitcoin codebase does not yet support some of
the necessary features to implement a full two-way peg, the `testnet` network
relies on a group of signatories (the "federation" part) to execute and verify
the redemption of testnet coins, while within Elements the network actually
utilizes a full two-way peg to redeem the outputs from testnet.

Let's take a look at what happens now.

### Redeeming Sidechain Tokens
To complete the loop, we need to get rid of our sidechain tokens, and restore
the original bitcoin we spent in creating them.  In our federated peg, we rely
on the federation to verify these, but once bitcoin supports the types of smart
contracts we need, it'll be completely two-way in both directions.

Generate yourself a mainchain wallet to receive the restored bitcoin:
```bash
./contrib/sidechain-manipulation.py generate-one-of-one-multisig mainchain-wallet
One-of-one address: mm8UW9YsjeHoVhXbHG4hEFKJt52P5iB7Vi
P2SH address: 2MzqiCCUwtKKEV9Kxiyvk8ZuNCFKbcbneva
```

Finally, provide the P2SH address you just created above to the
`send-to-mainchain` command, and the amount you wish to move (this can be any
subset of the amount you moved in earlier, but no more):
```bash
./contrib/sidechain-manipulation.py send-to-mainchain 2MzqiCCUwtKKEV9Kxiyvk8ZuNCFKbcbneva 1
```

That's it!  We've spun up both a Bitcoin node on the `testnet3` network, and an
Elements node on the `alpha` network.  We've moved `testnet3` bitcoin into the
`alpha` sidechain, moved it around, and finally returned ourselves to `testnet3`
bitcoin.

There's a ton of other things that Elements provides, including Segregated
Witness and Confidential Transactions.  Now that you have an Elements node
running, you can explore these things and more on your own.  We'll cover these
in more detail in the future!

Until then, please share what you build and help us by reporting any issues you
find on [the official Elements GitHub repo][elements github].  We're excited to
see what you build!

[presentation]: https://people.xiph.org/~greg/blockstream.gmaxwell.elements.talk.060815.pdf
[elements]: http://elementsproject.github.io
[testnet faucet]: https://testnet-faucet.elementsproject.org/
[elements github]: https://github.com/ElementsProject/elements
