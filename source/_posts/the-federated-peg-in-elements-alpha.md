title: The Federated Peg in Elements Alpha
date: 2016-02-29 23:30:04
---
The federated peg is the mechanism we use in Elements Alpha and Liquid to transfer coins from Bitcoin to sidechain and back.
While the high level design has been described in the [sidechains whitepaper](https://blockstream.com/sidechains.pdf) this post focuses on the actual implementation.

The federated component means that the transferred coins are locked on the main chain using a multisig output controlled by a federation of signers instead of an SPV-lock.
The peg mechanism doesn't require more than introducing two new opcodes to the Script language and is
designed to ensure that it can be easily soft-forked into Bitcoin in order to evolve to the full SPV peg.
<!-- more -->


### OP_WITHDRAWPROOFVERIFY (OP_WPV)
Let's start with Alpha's genesis block.
It looks very much unlike Bitcoin's genesis block because it creates exactly one output with a value of 21 million.
The output has the following scriptPubKey:

{% codeblock %}
6fe28c0ab6f1b372c1a6a246ae63f74f931e8365e15a089c68d6190000000000
9eac001049d5c38ece8996485418421f4a01e2d7
OP_WITHDRAWPROOFVERIFY
{% endcodeblock %}

This output is called *withdraw lock* because it represents the coins in the main chain which can be unlocked with a withdrawal.
OP_WITHDRAWPROOFVERIFY (OP_WPV) is a new opcode.
Note that there is no mining block reward in Alpha, so our only chance to obtain coins in Alpha at this point is to spend this withdraw lock.
Let's create a transaction we call *withdrawal transaction* that does just that.

OP_WPV expects the following elements on the stack:
1. HASH160(secondScriptPubKey), the secondScriptPubKey is used to extend checks
2. genesis block hash of the chain the withdraw is coming from
3. the coinbase tx within the locking block
4. the index within the locking tx's outputs we are claiming
5. the locking tx itself
6. the merkle block structure which contains the block in which the locking transaction is present
7. The contract which we are expected to send coins to
8. The scriptSig used to satisfy the secondScriptPubKey
9. secondScriptPubKey

The first two arguments are already provided by the scriptPubKey. They add chain specific information - in this case a scripthash we will explain later and bitcoin's genesis block hash.

The next arguments provide a 'locking transaction'.
This is the main chain transaction that locks coins in order to withdraw them on the sidechain.
Figure 1 shows the relationship between the transaction types we've seen so far.
<a href="/img/the-federated-peg-in-elements-alpha/peg.png">
    <img style="width:100%;" src="/img/the-federated-peg-in-elements-alpha/peg.png" alt="peg figure"/>
</a>
The withdrawal transaction spends OP_WPV locked coins by referring to a lock on the other chain.
Instead of using OP_WPV, the main chain lock is a multisig output controlled by the federation.
Note the symmetry of vocabulary: coins which are currently unlocked in the main chain are locked in the sidechain and vice versa.

The script interpreter tests if the destination of the locking transaction is really the federation. It further checks that the locking tx and coinbase tx are contained in the merkle block structure and reads the block height from the coinbase.
Elements Alpha uses an asymmetric peg and therefore a full Alpha node is expected to be a full validator of the parent chain as well.
In order to verify that the locking transaction is in the Bitcoin blockchain, Alpha connects to bitcoind via RPC (this is turned on with command line argument `-blindtrust=false`) and calls `getblock` with the merkle block's hash to check if it is has at least 10 confirmations (*confirmation period*).
In the future, OP_WPV will in addition accept an SPV proof to check without relying on bitcoind if the block has received enough confirmations (under some assumptions about the distribution of hash rate).

Next, OP_WPV expects the destination *contract* consisting of a 16 byte nonce and a 20 byte script hash that represents the receiver of the withdrawal transaction.
The interpreter checks that the locking transaction commits to the contract using the [pay-to-contract (P2C)](https://arxiv.org/pdf/1212.3257.pdf) construction.
P2C allows the sender of the locking tx to transparently specify the destination script hash, such that the validators can check the intended recipient of the withdraw. This works by deriving a new keypair for contract `x`: `privkey = old_privkey + H(x), pubkey = old_pubkey + H(x)*G`.

So, in summary, a user who wants to spend an OP_WPV locked output would first create a P2SH address on the side chain and assemble a main chain locking tx that sends the desired value to the federation. Then the user would embed her script hash (in the form of a contract) into the locking transaction and broadcast it. As soon as the confirmation period is over, the user can spend OP_WPV by providing the locking tx and the contract.


### Withdraw output
OP_WPV is a new type of opcode which has access to the outputs of the transaction that spends it.
In the case of OP_WPV, it checks that the transaction has two outputs: an output we call *withdraw output* and a OP_WPV-locked output to represent the change.
Next, the interpreter compares the output values, verifies that there is no more value in the
withdraw output than in the parent chain lock and that the remaining value goes back into
the lock output.
This change can then be unlocked later with another withdrawal transaction similar to the transaction we are creating here.

A withdraw output has the following scriptPubKey:
{% codeblock %}
OP_IF
    <nLockHeight>
    <lockTxHash>
    <nLocktxOut>
    <fraudBounty>
    <HASH160(secondScriptPubKey)>
    <genesisHash>
    OP_REORGPROOFVERIFY
OP_ELSE
    144
    OP_CHECKSEQUENCEVERIFY
    OP_DROP
    OP_HASH160
    <HASH160(destinationScript)>
    OP_EQUAL
OP_ENDIF
{% endcodeblock %}

Let's first look at the ELSE branch.
[OP_CHECKSEQUENCEVERIFY](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki) ensures that this branch is only executable if the withdraw output is buried at least 144 blocks deep in the blockchain (*contest period*).
After the contest period the withdraw output effectively becomes a regular P2SH script.
The interpreter additionally makes sure that the destination scriptHash is exactly the scriptHash from the contract that was committed to in the locking transaction.

Successful execution of the first branch requires providing a *fraud proof* to the second new opcode, OP_REORGPROOFVERIFY (OP_RPV).
Therefore, during the contest period the withdraw output allows any node to provide a fraud proof, spend the output and consequently collect a fraud bounty.

### OP_REORGPROOFVERIFY (OP_RPV)
OP_RPV is intended to correct invalid states of two types: double spends of a parent chain lock and parent chain reorganisations.
You might have realized already that the former situation is indeed not covered by OP_WPV alone. In fact, it is possible that withdrawal transactions which refer to the same parent chain lock make it into the chain.
Figure 2 shows the resolution of such a double spend attempt.
<a href="/img/the-federated-peg-in-elements-alpha/peg-fraud.png">
    <img style="width:100%;" src="/img/the-federated-peg-in-elements-alpha/peg-fraud.png" alt="peg figure"/>
</a>
OP_RPV allows to spend the withdraw output when a fraud proof is provided. It consists of the original withdraw transaction, the double spending withdraw transaction and a merkle block for each. The reference to the main chain lock is already given by the withdraw output.
In consequence, the interpreter then checks that there is indeed a double spend, both merkle blocks are valid and contain the transactions, and that the double spending withdraw transaction is newer than the original withdraw transaction.
Because blockchain consensus in Elements Alpha is determined by a federation of signers, the interpreter only requires the blocks to have valid signatures.
If Alpha was backed by PoW, OP_RPV would require SPV proofs to verify that the blocks are at the specified height similar to the SPV extension in OP_WPV's case.

Just like OP_WPV, OP_RPV peeks into the outputs of the transaction spending it. The transaction must have one output that uses OP_WPV to re-lock the withdraw output value minus the fraud bounty. The fraud bounty can be claimed by the prover.

As the name implies, OP_RPV does not only come into play when there is a double spend, but also when the parent chain reorganizes.
In such a situation, the locking transaction is either in another block or completely missing in the chain.
In any case, the withdraw output should be invalidated by a reorganisation proof.
This is not yet implemented in Alpha, but in principle the prover would provide an SPV proof that there exists a chain with sufficiently more work which does *not* include the block the withdrawal was coming from.

If alphad is started with the `tracksidechain=all` command line argument it stores all previously spent main chain lock outputs in order to issue fraud proofs if a double spend occurs.

Lastly, let's have a look at the curious secondScriptPubKey, which is expected to be the 9th argument to OP_WPV and is committed to in a withdraw lock (1st argument).
The secondScriptPubKey is executed with a stack that contains the result of the scriptSig execution and information about the withdrawal transaction, i.e. transaction fee, fraud bounty, the OP_CSV locktime (from the withdrawoutput’s scriptPubKey ELSE case) and a constant dummy byte string.
In Elements Alpha, the secondScriptPubKey for the Bitcoin lock is `OP_DROP 144 OP_LESSTHANOREQUAL`, which effectively ensures that contest period has passed.
The secondScriptPubKey does not inspect the result the of the secondScriptSig, so the default scriptSig in this case is just a one byte push.
This mechanism could in principle enforce additional chain specific limits on transaction fee and fraud bounty or more complex rules.


### Withdrawing from the sidechain
The mechanism behind sending coins from the sidechain to the main chain is - as far as the Alpha code is concerned - relatively simple.
Figure 3 shows the sequence of transactions during a withdrawal to the main chain.
<a href="/img/the-federated-peg-in-elements-alpha/peg-out.png">
    <img style="width:100%;" src="/img/the-federated-peg-in-elements-alpha/peg-out.png" alt="peg figure"/>
</a>
The federated lock on the main chain is a m of n multisignature output.
Functionaries who hold the lock run a program we call *watchman* which communicates to alphad via RPC and is responsible for releasing the lock when a withdraw request appears on the sidechain.
Note that due to the P2C payments, the federation is is not aware of a lock as long as the corresponding withdraw transaction has not taken place. This is because only the withdraw transaction reveals the data necessary - the contract - to derive pub- and privkey of the lock.

Withdraw requests take the form of a lock output, so a transfer from side- to main chain would be initiated by a new transaction with the following scriptPubKey:
{% codeblock %}
<HASH160(scriptDestination)>
OP_DROP
<genesisBlockHash>
<HASH160(secondScriptPubKey)>
OP_WITHDRAWPROOFVERIFY
{% endcodeblock %}
The script puts the coin in a regular sidechain lock and additionally communicates the main chain destination. This instructs the functionaries to spend their lock and credit the intended receiver.

Behind the scenes watchman follows a round-based distributed protocol (using a separate network) to select a round-leader, who is responsible for collecting withdraw requests and creating a corresponding main chain withdraw transaction.
The other functionaries check that the transaction correctly spends the withdraw requests (i.e. it goes to the correct destination, the sidechain lock has at least n confirmations, etc.) and sign it.
If enough signatures can be collected, the withdrawal transaction is valid and broadcast to the bitcoin network.

The federation has to pay the transaction fees, so there are several ways for users to donate, like creating OP_RETURN outputs on the sidechain or sending coins directly to the federation's address (instead of P2C).


### Conclusion
Alpha's peg mechanism allows to freely transfer coins between Bitcoin and federated sidechains. Main chain locks are controlled by a federation whereas sidechain locks are secured by main chain consensus ("asymmetric peg") and sidechain consensus.

The new opcodes OP_WPV and OP_RPV can be easily adapted to allow a symmetric peg instead of requiring full validation of the main chain and additionally to support PoW as the sidechain consensus algorithm.
This capability and the fundamental design decision to follow the 'Zen of Bitcoin' by avoiding non-local state in the script interpreter opens the door to soft-forking the peg mechanism into Bitcoin itself.
