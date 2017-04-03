---
title: Confidential Assets
description: Extend security to multiple asset types while obscuring which ones are in use in specific transactions.
---

## Summary

*Principal Investigator: Andrew Poelstra*

The security of any blockchain ledger comes down to public verifiability of
two properties of every transaction: that they are authorized by all required
parties, and that they do not affect the total currency supply. In Bitcoin,
the latter property is so simple to check that it often goes unremarked: add
up the total output amount and total input amount and compare them. With the
development of [Confidential Transactions (CT)](/confidential-transactions/),
however, this security property is front and center, as it must be preserved
despite all amounts being cryptographically blinded.

Several blockchain technologies have gone beyond Bitcoin to support multiple
asset types on the same chain. This allows a wider set of users to share the
security properties of the same chain, and also enables new use cases, such
as multi-asset transactions which effect atomic exchanges. Enabling this is
as simple as labelling each transaction output with a publicly visible "asset
tag"; however, this would expose information about users' financial behavior,
undermining the privacy benefits of CT. **Confidential Assets (CA)** is a
technology to support for multiple asset types while blinding all asset tags,
preserving the privacy of CT while extending the power and expressibility of
blockchain transactions.

As in CT, Confidential Assets allows anybody to cryptographically verify that
a transaction is secure: the transaction is authorized by all required parties
and no asset is created, destroyed or transmuted. However, only the
participants in the transaction are able to see which asset types were used
and in what amounts.

In a multi-asset chain, it may make sense in some contexts for assets of a
specific type to be created or destroyed. This is accomplished by means of
*issuance transactions*, which create new asset tags and a specified amount
of this asset. Later reissuance or deissuance may be done by proving ownership
of *issuance tokens*, which are related (but distinct) assets. Issuance tokens
may be created alongside a given asset type, or not, if the asset should not
support reissuance.

Issuance transactions are unique in that they are not required to balance to
zero. However, if they issue a public amount, it is still verifiable that
exactly this amount, no more and no less, was actually issued.

## Technology Behind Confidential Assets

### Asset Tags and Rangeproofs

To describe the technology behind CA, we start with the (Pedersen commitments
that [form the basis of Confidential Transactions](/confidential-transactions/):
```
commitment = xG + aH
```
where `G` is a standard generator of an elliptic curve and `H` is a second
generator for which nobody knows the discrete log with respect to `G`. We call
such a generator nothing-up-my-sleeve, or NUMS.

In CT, this was described as committing to `a` coins with a blinding factor of
`x`. We observe that if we refer to the generator `H` as a coin we can read the
term `aH` algebraically as "`a` coins". When `H` is our only generator this is
merely a semantic trick. But suppose we add another NUMS generator `I`, and
consider the two commitments
```
commitment_1 = xG + aH
commitment_2 = xG + aI
```
Now we can think of `H` and `I` as representing two distinct assets, and we see
that these two commitments, while committing to the same amount, are commitments
to different assets.

Consider now a complete transaction with two inputs of distinct asset types
and two outputs, like so

```
in1 = xG + aH, H --\   /-- uG + cH, H = out1
                   |---|
in2 = yG + bI, I --/   \-- vG + dI, I = out2
```
In CT, where we had only one generator, we required the equation
```
out1 + out2 - in1 - in1 = 0
```
to hold, which it would if and only if the transaction balanced. As it turns
out, this same equation works even with multiple assets:
```
0 = out1 + out2 - in1 - in1
  = (uG + cH) + (vG + dI) - (xG + aH) - (yG + bI)
  = (u + v - x - y)G + (c - a)H + (d - b)I
```
Since `H` and `I` are both NUMS points, the only way for this equation to hold
is if each individual term is 0, and in particular, if `c = a` and `b = d`. In
other words, this equation holds only if the total amount of asset `H` is the
same on the input side as on the output side **and** the total amount of asset
`I` is the same on the input and output side.

This extends naturally to more than two asset tags; in fact, it is possible to
support an unlimited number of distinct asset types, as long as each one can
be assigned a unique NUMS generator.

As in CT, this simple equation is insufficient because it is possible for amounts
to overflow, effectively allowing negative-valued outputs. As in CT, this can be
solved by attaching a rangeproof to each output, in exactly the same way. The only
difference is that the verifier must use the appropriate asset tag in place of
the fixed generator `H`.

### Blinded Asset Tags and Asset Surjection Proofs

The above discussion assumed every transaction output had a NUMS generator, or
asset tag, associated to it, and that outputs of the same asset type would use
the same tag. This does not satisfy our privacy goals because it is visible
what type of asset every output represents.

This can be solved by replacing each asset tag with a _blinded asset tag_ of
the form
```
A = H + rG
```
Here `H` is an asset tag from above and `r` is a secret random value. Anybody
who knows `r` can tell what asset this tag represents, but to anyone else it
will appear to be a uniformly random elliptic curve point. We see that any
commitment to a value with `A` is also a commitment to the same value with
`H`, so our "outputs minus inputs equals zero" rule will continue to work
when validating transactions:
```
commitment_A = xG + aA = xG + a(H + rG) = (x + ra)G + aH = commitment_H
```
The introduction of this blinding factor does not affect the user's ability
to produce a rangeproof, though it does make the algebra slightly more
complicated when constructing the transaction to balance out to zero.

However, since every blinded asset tag looks uniformly random, how can
verifiers be sure that the underlying asset tags are legitimate? It turns
out that the "sum to zero" rule is not sufficient to prevent abuse. For
example, consider the "blinded asset tag"
```
A' = -H + rG
```
Any amount of the blinded asset `A'` will actually correspond to a _negative_
amount of asset `H`, which an attacker could use to offset an illegal
increase of the money supply.

To solve this problem we introduce an _asset surjection proof_, which is a
cryptographic proof that within a transaction, every output asset type is
the same as some input asset type, while blinding which outputs correspond
to which inputs.

The way this works is simple. If `A` and `B` are blinded asset tags which
commit to the same asset tag `H`, say, then
```
A - B = (H + aG) - (H + bG) = (a - b)G
```
will be a signature key with corresponding secret key `a - b`. So for a
transaction output `out1`, we can use a ring signature (proof that one of
several secret keys is known that keeps secret which one) with the keys
`out1 - in1`, `out1 - in2`, and so on for every input in the transaction.
If `out1` has the same asset tag as one of the inputs, the transaction
signer will know the secret key corresponding to one of these differences,
and be able to produce the ring signature.

The asset surjection proof consists of this ring signature.

### Future Work

Because algebraically, Confidential Assets is such a straightforward
extension of Confidential Transactions, many of the tools developed for
use with CT can be used with few modifications with CA, giving them the
power to confidently and confidentially handle multi-asset transactions.
Examples of such technologies are 

- ValueShuffle (add link, also check with Tim if the name has changed)
- [MimbleWimble](http://diyhpl.us/~bryan/papers2/bitcoin/mimblewimble.txt)
- [Scriptless Scripts](https://download.wpsoftware.net/bitcoin/wizardry/mw-slides/2017-03-mit-bitcoin-expo/slides.pdf)

We are looking forward to the future, as many exciting developments
continue to appear.


