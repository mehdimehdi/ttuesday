---
layout: post
title:  "Proof of work"
date:   2017-09-20 01:05:41 -0700
---

The blockchain is the information architecture that allows us to store the ledger for peer-to-peer cash. And the proof-of-work is the assurance that the ledger is acutally valid. The idea was borrowed from Adam's Back Hashback [1]. It uses the notion of letting adding to the block in the blockchain a proof that a really hard computational work has been done. It "proves" that very complicated "work" has been done, hence 'proof-of-work'. The main driver for this is to make it very hard to counterfeit to blocks in the block chain. And another notion that is important is that it's harder to counterfeit older entries in the block chain. The proof-of-work means it's really hard to counterfeit the the block, it also means that it cost money (electricity needed to run the computers to come up with the proof-of-work), this is when the right [incentives](/2017/09/16/incentives-against-fraud.html)  becomes important.

What is actually the hard problem that constitute "proof-of-work"?

Let's start with a cryptographic hash function. It's a function (a small program that computer understand) that can take any message as an input and produce as an output a sequence of bits. 
Here are a few properties for a cryptographic has function:
 1. The output has a fixed length.
 2. The content of the ouput will completely change even if the input change just a tiny bit.
 3. The content of the output looks completely random compare to input, and figuring out the input based on the output is pretty much infeasible.

sha256 is the basic crypographic hash function that will be used for our 'proof-of-work'. Here is how it works:

sha256('hello') = ''
sha256('hell0') = ''


See! Completely different results, for very similar input. Thanks to the 3rd property above, if we are given the output of that function, and wanted to come up with the message that was the input, there is not better way than try every possible guess of the function, and scan each of the response to see if it's the same as the output that we want to match.

* Solves a very hard problem and be -> because it's 
* rewarded
* dumb work: useless
