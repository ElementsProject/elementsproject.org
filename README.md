![Sidechain Elements logo](http://i.imgur.com/Vbhiqop.png)

Elements is an open source collaborative project where we work on a collection of experiments to more rapidly bring technical innovation to Bitcoin.  Elements are features that are proposed and developed in this technical community that in arbitrary combinations can be fashioned into sidechains.

[![Greg Maxwell's Sidechain Elements Intro Video](http://i.imgur.com/AsSENaW.png)](http://www.blockstream.com/developers/)

“It's nice working on something without millions of BTCs resting on it, and still have a path to production use.”

## Current Elements
These are the features currently under investigation as part of the Alpha dev sidechain.

####Confidential Transactions 
*Principal Investigator: Greg Maxwell* [[_Peer reviewed technical details_](https://github.com/ElementsProject/elementsproject.github.io/blob/master/confidential_values.md)]

One of the most powerful new features being explored in Elements is Confidential Transactions. This keeps the amounts transferred visible only to participants in the transaction (and those they designate), while still guaranteeing that no more coins can be spent than are available in a cryptographic way.

This goes a step beyond the usual privacy offered by Bitcoin’s blockchain, which relies purely on pseudonymous - but public - identities. This matters, because insufficient financial privacy can have serious security and privacy implications for both commercial and personal transactions. Without adequate protection, thieves and scammers can focus their efforts on known high-value targets, competitors can learn business details, and negotiating positions can be undermined. 

The most visible implication of Confidential Transactions is the introduction of a new address type (confidential addresses). These are longer than usual as they also includes a blinding key for the values. They are the default address type in Alpha.

#### Segregated Witness
*Principal Investigator: Pieter Wuille*

In Alpha, the specification of a transaction’s effects on the ledger is separated from the data necessary to prove its validity (called a witness in cryptography). This completely eliminates all known forms of transaction malleability, and allows significant blockchain pruning optimizations.

In Bitcoin, transactions contain both information about the effect on the ledger (UTXOs being spent, addresses, and amounts involved) and data proving that the transaction is authorized (input signatures). For Witness Segregation, transaction IDs are redefined to only depend on the effect information, and blocks commit separately to the witness data. This has several advantages:
* Bitcoin has seen some “Normalized Transaction ID” proposals, but these are effectively subsumed by Segregated Witness, which is both more efficient and more usable, as Normalized Transaction ID mechanisms still require rewriting dependent transactions after inputs are malleated. Such normalization is a necessary building block for higher-layer protocols such as Lightning.
* As transaction IDs no longer cover the signatures, they remove all forms of transaction malleability, in a much more fundamental way than BIP62 aims to do. This results in a larger class of multi-clause contract constructs that become safe to use.
* Potential for more efficient SPV output creation proofs (used by lightweight clients), as the signatures can be omitted from the transaction data without breaking the Merkle tree structure.
Potential for nodes that do not wish to store or verify old transaction signatures, to remove the witness data from disk or not transfer it at all even, reducing blockchain storage/bandwidth amounts by a large factor. In Alpha, the witness data size is even more significant than in Bitcoin, as it also includes large range proofs for the output values.

#### Relative Lock Time
*Principal Investigator: Mark Friedenbach*

The consensus-enforced semantics of the sequence number field is modified to enable a signed transaction input to remain invalid for a defined period of time after confirmation of its corresponding output, for the purpose of supporting consensus-enforced transaction replacement features.

Bitcoin has sequence number fields for each coin a transaction is spending. The original idea appears to have been that the highest sequence number should dominate and miners should prefer it over lower sequence numbers. This was never really implemented, and the half implemented code seemed to be making the assumption that miners would honestly prefer the higher sequence numbers, even if the lower ones were much more profitable. That turns out to be a dangerous assumption, and so most have assumed that kind of sequence number mediated replacement was useless because there was no way to enforce "honest" behaviour, as even a few rational (profit maximizing) miners would break that completely. This change provides the missing piece that makes sequence numbers do something with respect to enforcing transaction replacement without assuming anything other than profit-maximizing behaviour on the part of miners. A new opcode is added which enables Bitcoin scripts to check these constraints, CHECKSEQUENCEVERIFY.

Relative lock-times can be used for all the same purposes as regular (absolute) lock-times, such as time-locked escrow services, but the relative form is of particular interest in applications where the blockchain is used as a communication medium. For example, the contest period of the two-way peg is most naturally expressed as a relative lock-time condition beginning with the transaction announcing the proof of withdraw.

#### Schnorr Signature Validation
*Principal Investigator: Patrick Strateman*

Instead of DER-encoded ECDSA signatures over the secp256k1 curve, the CHECKSIG and related operators now use densely packed Schnorr signatures over the same curve. The advantages are:
* Efficient threshold signatures for n-of-n. Multiple Schnorr signatures can be combined to end up with a signature valid for the sum of the public keys, so arbitrarily large n-of-n multisig can be done by only communicating the single sum signature, which can be verified with a single CHECKSIG operation.
* Smaller signatures (64 bytes instead of 71-72) with none of the problems that DER encodings have caused for Bitcoin.
Potential support for batch validation (up to a factor 2 speedup to verify groups of 32 signatures at once). This requires knowing the R.y coordinate (ECDSA ignores this) and at the script level, guaranteeing that all signature verification failure results in script failure (i.e., all CHECKSIG operators behave like CHECKSIGVERIFY).
Stronger security proof.
* Provably no inherent signature malleability, while ECDSA has a known malleability, and lacks a proof that no other forms exist. Note that Witness Segregation already makes signature malleability not result in transaction malleability, however.
* Slightly faster to sign/verify than ECDSA.

#### New opcodes
*Principal Investigator: Patrick Strateman*

Alpha enables several new script opcodes, in addition to the ones already supported by Bitcoin.
* Disabled opcodes. Bitcoin used to support a wider range of Script opcodes than exist now. Many were disabled for security reasons in 2010, and require a hard fork to re-enable them. Some of them had significant risks (unbounded memory usage), but not all of them. Alpha reintroduces these safe but disabled opcodes. They include string concatenation and substrings, integer shifts, and several bitwise operations.
* A new DETERMINISTICRANDOM operation which produces a random number within a range from a seed.
* A new CHECKSIGFROMSTACK operation which verifies a signature against a message on the stack, rather than the spending transaction itself.

These new opcodes have several use cases, including double-spent protection bonds, lotteries, merkle tree constructions to allow 1-of-N multisig with huge N (thousands), and probabilistic payments.

#### Signature Covers Value
*Principal Investigator: Glenn Willen*

The signatures verified by the CHECKSIG operators now cover the output value of spent inputs. This avoids the need for hardware signing devices to know the full previous transactions whose outputs are spent; if they are being lied to, the resulting signature is invalid anyway.

A side effect of this change is that signing now needs to know the values (blinded or not) consumed by the transaction’s inputs.

#### Deterministic Pegs
*Principal Investigator: Matt Corallo*

Deterministic pegs allow Elements Alpha to carry redeemable testnet coins without any modifications to testnet itself. Transfers into Alpha are validated by all full nodes, optionally with the assistance of an RPC call to a testnet node to validate blockchain membership without the presence of compressed SPV proofs in testnet. Transfers out of Alpha are performed by a federation of functionaries which are trusted to hold the coins for Alpha.

Sidechains, like other alternative chains, can also be secured by merge-mining.  However during a bootstrap period of introduction of a new chain, unless the start of merge mining were very well synchronised, there will be a period of lower hashrate. During the early stages of this bootstrap the chain could have low enough hashrate to present a security risk even against a modest powered attacker. Given the challenges of synchronising something as organic and decentralised by design as bitcoin mining, we therefore need a mechanism to bootstrap chain security.  We start in this release with a threshold of functionaries and are plan for a later version to phase in merge-mining.

#### Signed blocks
*Principal Investigator: Jorge Timón*

SHA256d proof of work is replaced with the system’s scripting system, just signing blocks instead of transactions. In other words, the Dynamic Membership Multi-party Signature (DMMS) is replaced with a (Static Membership) Multi-party Signature. This has also been described in the past as “private chains” [http://freico.in/docs/freimarkets.pdf ].

The Elements Alpha release uses a threshold of functionaries as a protocol adaptor and also to sign blocks of transactions.  In a future release we plan to replace the block-signing with merge-mining, though the functionaries remain to communicate the transfer transactions to the main chain.   The Signed Blocks feature serves to provide transaction processing functionality until merge-mining is implemented.  Our intent is to later phase in the fully decentralised 2-way peg mechanism to replace the functionaries.

## Proposed Elements
These are some of the features currently under development, but are yet ready for testing in dev sidechain.

#### Basic Asset Issuance
*Principal Investigator: Jorge Timón*
 * [feature branch multi-asset-0.10](https://github.com/ElementsProject/elements/tree/multi-asset-0.10) - branch of ongoing assets dev

Users can issue their own assets which represent fungible ownership of the underlying asset type representing by the newly created units, which could theoretically represent any asset including vouchers, coupons, currencies, deposits, bonds, shares, etc (subject to the respective jurisdiction’s regulatory requirements. 

This opens the door for building trustless exchanges, options, and other advanced smart contracts involving those arbitrary assets and the “hostcoin” (a native asset whose ID is equal to the hash of the genesis block or chain ID; in Alpha’s case, it is the federated-peg coin which is backed by testnet coins, see “Deterministic peg” section).

All outputs are tagged with their asset identifier. Consensus rules are modified so that the total inputs and outputs are checked separately per asset.
A new transaction type is added for creating issued assets (asset definition transactions). Like coinbase transactions, asset definition transactions (the new transaction type) have a null input, but unlike coinbases, asset definition transactions have more inputs in addition to that first null input. This difference not only helps us distinguish between the two: it also guarantees a source of entropy for the asset id (which is the sha256d hash of the transaction). Within an asset definition transaction, any number of outputs with 0 as asset ID can be included with any amount and they will be treated as the initial unspent outputs for the newly created asset.

This technology is similar to colored coins in many ways, but explicit and consensus-enforced tagging has many advantages:

* Supports SPV wallets much more efficiently.
* Allows more complex consensus-enforced contracts.
* Benefits from other consensus-enforced extensions (ie confidential transactions would not be compatible with colored coins on top of Alpha).
* Opens the door for further consensus-enforced extensions that rely on the chain being able to operate with multiple assets.

Currently only the hostcoin can be used to pay fees, but it should be possible to pay fees of different asset types simultaneously.
In this first version all units of a given type must be issued within the asset definition transaction. In future versions it will be possible to define assets with a dynamic supply that can be increased after the definition, allowing the issuer to create new units.
Future versions can also implement consensus enforced interest that would be interesting for p2p lending and issuance of assets with built-in demurrage (negative interest) among other things.

#### Bitmask Sighash Modes
*Principal Investigator: Glenn Willen*
 * [feature-bitmasksighash](https://github.com/ElementsProject/elements/tree/feature_bitmasksighash) - EXAMPLE branch of Bitmask Sighash modes

The new CHECKSIG2 operator allows arbitrary, miner-rewritable bitmasks of inputs and outputs. This allows for more complex contractual pre-commitment schemes, such as signed offers with change in a distributed asset exchange.

# Testnet Dev Sidechain Demo: Elements Alpha
To make it easy for the community to test the latest Elements, this project combines the best of them into dev sidechains.  The first release is Elements Alpha, a developer sidechain and network that introduces several new technologies on a sidechain, pegged to Bitcoin’s testnet. All code is open source, like Bitcoin itself, and others are encouraged to contribute to the project as we work to improve and add additional Elements.  Elements Alpha is intended to be a technology demo and testing environment.  Proposed Elements were not ready, and as a testnet development sidechain, this blockchain is intended to be short-lived and easily replaced as the technology evolves.

Elements Alpha functions as a sidechain to Bitcoin’s testnet, though the peg mechanism currently works through a centralized protocol adapter, as described in the Sidechains whitepaper in appendix A. It relies on an auditable federation of signers to manage the testnet coins transferred into the sidechain (see the Deterministic Peg feature) and to produce blocks (see the Signed Block feature). This makes it possible to immediately explore the new chain’s possibilities, using different security trade-offs. We plan to, in a later release, upgrade the protocol adapter to support fully decentralized merge-mining of the sidechain, and ultimately to phase in the full 2-way pegging  mechanism.

#### Source Code
* https://github.com/ElementsProject/elements - contains isolated feature and dev sidechains braches
 * [branch alpha](https://github.com/ElementsProject/bitcoin/tree/alpha) - testnet dev sidechain demo

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


#### Contributors and Sponsors
[![Blockstream](https://static2.blockstream.com/wp-content/themes/blockstream/assets/images/logo-dark.png)](http://www.blockstream.com/)

Sidechain Elements is an Open Source project sponsored by Blockstream, with contributions from @apoelstra, @gmaxwell, @gwillen, @jonasschnelli, @jtimon, @jwilkins, @kanzure, @Luke-Jr, @maaku, @petertodd, @pstratem, @sipa, @TheBlueMatt, @wtogami
