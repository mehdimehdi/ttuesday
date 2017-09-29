---
layout: post
title:  "Cryptographic gimmick as a proof of work"
date:   2017-09-27 01:05:41 -0700
---

The blockchain is the information architecture to store a ledger for peer-to-peer cash. The proof-of-work is the process that assures that the ledger is acutally valid. The idea was borrowed from [Adam's Back Hashback](http://www.hashcash.org/papers/hashcash.pdf) [PDF]. Proof that a really hard computational work was performed is added to the block in the blockchain, hence 'proof-of-work'. The goal is to make it very hard to counterfeit blocks in the blockchain. Moreover, it's harder to counterfeit older blocks in the blockchain, because one would have to counterfeit all the blocks linked after the counterfeited block, which requires a lot more work. Computing the proof-of-work costs money (electricity needed to run the computers to come up with the proof-of-work), this is why introducing the right [incentives](/2017/09/16/incentives-against-fraud.html) for doing the proof-of-work (mining) becomes important.

**What is actually the hard problem that constitutes "proof-of-work"?**

Let's start with defining what is a cryptographic hash function. It's a function (a small program that computers understand) which can take a message in (input) and generates a sequence of bits out (output or hash). 

The important properties of a cryptographic hash function are:
 1. The output has a fixed length, no matter the input.
 2. The content of the ouput will completely change even if the input changes just a tiny bit.
 3. The content of the output looks completely random compare to the input, and discovering the input based on the output is pretty much [infeasible](http://www.hashcash.org/papers/hashcash.pdf).

`sha256` is a classic crypographic hash function that is used for bitcoin 'proof-of-work'.

```
sha256('hi')='8f434346648f6b96df89dda901c5176b10a6d83961dd3c1ac88b59b2dc327aa4'
sha256('h1')='33112ee14ee469c3eb52fe90322ec81dd404a0093d565a6d71ce77cbc8124e3b'
```


Completely different results for very similar inputs! 

If we were given an output of that function, and wanted to come up with the message that was the input, there would be no better way than guessing an input, verifying if it matches the output expected. If it matches: we got it! if it doesn't match, try to guess a different input. Repeat this until we find it.

For example if the goal was to find what input generated the hash `8f434346648f6b96df89dda901c5176b10a6d83961dd3c1ac88b59b2dc327aa4`. 

Then we would have to try: 
```
sha256('0')='5feceb66ffc86f38d952786c6d696c79c2dbc239dd4e91b46729d73a27fb57e9'
sha256('1')='6b86b273ff34fce19d6b804eff5a3f5747ada4eaa22f1d49c01e52ddb7875b4b'
sha256('2')='d4735e3a265e16eee03f59718b9b5d03019c07d8b6c51f90da3a666eec13ab35'
...
sha256('a')='ca978112ca1bbdcafac231b39a23dc4da786eff8147c4e72b9807785afee48bb'
sha256('b')='3e23e8160039594a33894f6564e1b1348bbd7a0088d42c4acb73eeaed59c009d'
...
sha256('aa')='961b6dd3ede3cb8ecbaacbd68de040cd78eb2ed5889130cceb4c49268ea4d506'
sha256('hh')='72b289ec78e0a928c565480a435453e30acb92eddb3b78ff168b28737cf6a849'
sha256('hi')='8f434346648f6b96df89dda901c5176b10a6d83961dd3c1ac88b59b2dc327aa4'
#BINGO!
```

That simple fact that you have to scan through many different options in order to find your solution is turned into the gimmick to create the proof-of-work.

**How are cryptographic hash functions used to build the proof-of-work?**

Let's take our block example from our [blockchain post](/2017/08/28/double-spending.html):

```
--> hash of block A  -----------------> hash of block B  -------------------------> hash of block C
    * transaction 1                     * transaction 5                             * transaction 7
    * transaction 2                     * transaction 6                             * transaction 8
    * transaction 3                     * timestamp: 2017-08-23..                   * transaction 9
    * transaction 4                     * hash of block A                           * timestamp: 2017...
    * timestamp: 2017-08-23             * proof-of-work                             * hash of block B
    * hash of block Z                                                               * proof-of-work
    * proof-of-work
```


What we blindly called _'proof-of-work'_ in each of the blocks (A, B and C) are actually magic sets of characters. What makes them magic is that when `sha256` (our cryptographic hash function) is applied to the block data (list of transactions, timestamp, hash of previous block, and that magic set of characters). The output (hash) actually starts with a predefined set of 0.

A miner is tasked to come up with the set of characters where sha256(list of transaction + timestampe + hash of previous block + MAGIC SET OF CHARACTERS) = `00000000000000000001234AB14509..12BC`

As we have described before, the only way to come up with that magic set of characters is to try a lot of options. And hoping that after a while you will land on an set of characters that will generate a hash that starts with the set of 0.

This is how a miner actually claims they have mined the block. They tried many set of characters until they found one that meets the requirement. It's really easy for anyone to confirm that it is the right set of character: they just need run the sha256 function on the block information with that number, and they will instantly find the output to be starting with the predefined set of 0s. If not, the claim from that miner will be discarded.

**How hard is it to find that magic set of characters?**

Let's pick the predefined number of zero as 20. The result of the `sha256` function needs to start with 20 zeros. The probability of finding the magic set of character is 1/(2^20) about 1 in a million. That means that on average someone will need to try one million set of characters before they find the magic set of characters.

If the number of zeros is increased to 30, that number is one in a billion.

As you can already imagine, that predefined number of zero is configurable, and is adjusted to make the problem harder or simpler depending on how fast miners actually come up with the solution. The goal being to match one block mined every ten minutes.

This is our proof-of-work. It makes tricky use of cryptography to secure our blockchain and protect against double spending. It's very clever and at the same time uses an incredible amount of energy with the only purpose of securing our ledgers without the need for a trusted third party. Some say it's a waste of energy, others think that there might be more "useful" ways to create a proof-of-work that might be actually more useful to its users.
