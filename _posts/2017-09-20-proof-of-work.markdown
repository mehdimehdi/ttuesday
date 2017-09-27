---
layout: post
title:  "Proof of work"
date:   2017-09-20 01:05:41 -0700
---

The blockchain is the information architecture that allows us to store the ledger for peer-to-peer cash. And the proof-of-work is the process that assures that the ledger is acutally valid. The idea was borrowed from Adam's Back Hashback [1]. It uses the notion of adding to the block in the blockchain a proof that a really hard computational work has been done, hence 'proof-of-work'. The main driver for this is to make it very hard to counterfeit blocks in the blockchain. And another notion that is important is that it's harder to counterfeit older entries in the block chain, because one would have to counterfeit all the blocks linked after the counterfeited blocks, which requires a lot more work. Computing the proof-of-work costs money (electricity needed to run the computers to come up with the proof-of-work), this is when the right [incentives](/2017/09/16/incentives-against-fraud.html)  becomes important.

What is actually the hard problem that constitutes "proof-of-work"?

Let's start with defining a cryptographic hash function. It's a function (a small program that computer understand) that can take a message in (input) and generates a sequence of bits out (output). 

Here are a few properties for a cryptographic hash function:
 1. The output has a fixed length.
 2. The content of the ouput will completely change even if the input change just a tiny bit.
 3. The content of the output looks completely random compare to input, and figuring out the input based on the output is pretty much infeasible. 

sha256 is a basic crypographic hash function that will be used for our 'proof-of-work'. Here is how it works:

sha256('hello') = ''
sha256('hell0') = ''


Completely different results, for very similar input. Thanks to the 3rd property above, if we are given the output of that function, and wanted to come up with the message that was the input, there is not better way than try every possible guess of the function, and scan each of the response to see if it's the same as the output that we want to match. 

For example if the goal was to find what input generated the hash ''. Then we would have to try: sha256('0'), sha256('1'), sha256('2'), ..., sha256('a'), sha256('b'), ... , sha256('aaa'), ... sha256('helln'), sha256('hello') BINGO!


How are cryptographic has functions used to build the proof-of-work:

Let's take our block example from our (blockchain post)[/2017/08/28/double-spending.html]:

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


What we blindly called 'proof-of-work' in each of the blocks (A, B and C) is actually a magic set of characters. What makes it magic is that when sha256 (our cryptographic hash function) is applied to the the block data (list of transactions, timestamp, hash of previous block, and that magic set of character). The output (hash) actually starts with a predefined set of 0.

As we have described before, the only way to come up with that magic set of characters is to try a lot of options. And hoping that after a while you will land on an set of characters that will generate a hash that starts with the set of 0.

This is how a miner actually claims they have mined the block. The found that a right set of characters. It's really easy for anyone to confirm that it actually is the right set of character: the just need run the sha256 function on the block information with that number, and they will instantly find the output to be starting with the predefined set of 0s. If not, the claim from that miner will be discarded.

How hard is it, to find that magic set of characters?

Let's pick that the predefined number of zero is 20. The the result of the sha256 function needs to start with 20 zeros. The probably of finding the magic set of character is 1/(2^20) about 1 in a million. That means that on average someone will need to try one million times before they find the magic set of characters.

If the number of zeros is increased to 30, that number is a billion.
As you can already imagine, that predefined number of zero is configurable, and is setting that is adjusted to make the problem harder or simpler depending on how fast miners actually come up with the solution. The goal being to match one block mined every ten minutes.

This is our proof-of-work. It makes clever use of cryptography to secure our blockchain and protect ourselves against double spending. It's very clever and at the same time uses an incredible amount of energy with the only purpose of securing our ledgers without the need for a trusted third party. Some might say it's a waste of energy, others think that there might be more "useful" ways to create a proof-of-work that might be actually more useful to its users.
