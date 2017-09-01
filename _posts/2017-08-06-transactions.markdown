---
layout: post
title:  "Electronic peer-to-peer transactions"
date:   2017-08-05 21:05:41 -0700
---
> I'm not trying to explain or define bitcoin in this piece. I [like to study in small concrete pieces](/about) of a bigger concept in order to understand the whole picture. In this article I'm diving into the electronic peer-to-peer transaction piece of bitcoin. It's missing important and innovative parts. If one doesn't truly understand the peer-to-peer transaction piece, the whole picture will always look off. No matter how much time you spend on the innovative part of bitcoin.

Let's look at how a person-to-person transaction works in the real world. There is cash. Someone has that cash in their possession. They can decide to hand it over to someone else for exchange of goods or services.

To put in the most simple way, there are three properties:
1. The cash has a perceived value shared by both parties. (let's not worry about the notion of value for the purpose of this discussion)
2. Someone can prove it owns the cash, by the sole fact that the cash is in their possession. (Let's not worry about stolen cash, or counterfeit)
3. There is an easy way to transfer the cash to someone else.

In order to accomplish this in the electronic world, Satoshi Nakamoto has a few tricks:

Picture a list of transactions digitally recorded. Every transaction references the previous one (it's a chain of transactions). A transaction contains information about to the owner (the recipient of the transaction), a reference to the previous transaction (that's the link in the chain), and the proof that the previous owner has aggreed to do the transaction. When a new transaction is added, it references back to the previous transaction.

**That chain of transactions is an eletronic coin.** Why?

1. Because people perceive there is value in being the current (last) owner. [1]
2. Someone can 'prove' that he is the owner of the electronic coin. (we will briefly discuss how the proof is provided later).
3. There is a mechanism to transfer that electronic coin to someone else.

The leap of faith of believing that the chain of transactions is actual electronic cash is the hardest part. It feels fake, intangible, but at the end of the day, what makes you think that a piece of paper with "in god we trust" printed on it is actually cash? Because people around you also assign value to it.[2]

The concept is the same for electronic cash.

Satoshi wants us to use cryptogaphy to 'prove' ownership. An owner signs the transaction and adds the signature to a transaction when transfering ownership. In very short, "signing" is a mathematical method to create a list of characters that demonstrate the authenticity of any digital message or document; in our case the transaction.

Here is how a transaction works:

* Owner #1 is the current owner of the electronic coin.
* Owner #1 decides to transact and transfer the electronic coin to owner #2. 
* Owner #1 gets a public identifier of owner #2, a reference to the previous transaction (that describes how he became the current owner), and its own digital signature.
* A new transaction is created with all of that information.
* Owner #2 can verify that the signature is correct and is now the owner of the electronic coin.

If a malicious person claimed to be the owner of the coin, let's call him owner X. And he tries to transact, then owner #2 can look at the signatures in the chain of transactions and see if it all looks proper. If Owner X created the coin out of thin air, somewhere in the chain the signature will not match its respective owner.

With this method we can now prove ownership of electronic coin, transfer this coin. And no-one can fake ownership of the electronic coin.

The obvious major problem that Satoshi needs to address is the fact that the owner of the electronic coin can send multiple time the same electronic coin without being caught. That's called [double spending](http://ttuesday.com/2017/08/28/double-spending.html), and that's the main reason why banks play a role in our current system. Satoshi has a solution for this, and I'll cover this later, once I spend more time discussing the digital signature process in more details.

> _Thought experiment_:
> Without getting too utopian about the application of Satoshi's idea, but to give you sense of how powerful the concept is, try to change the words "electronic coin" with "digital asset" in this essay. Electronic coin limits the imagination to the cash metaphore, but digital asset can take us in a lot of different places.


Thanks to [Mohit](https://twitter.com/mohitmamoria) and [Stan](https://twitter.com/spolu) for review drafts of this.

[1] Being the current owner of a coin use to be priced at a few cents in 2010 to over $3000 in early August 2017.  
[2] USD is not backed by gold since 1971.
