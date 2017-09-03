---
layout: post
title:  "Blockchain against double spending"
date:   2017-08-28 18:00:00 -0700
---

We created [electronic cash out of bits](http://ttuesday.com/2017/08/05/transactions.html) and used [digital signatures](http://ttuesday.com/2017/08/16/cryptography.html) to authenticate recipients of transactions without requiring a central trusted authority. We also know that we have one problem that we haven't solved quite yet: double spending.

**Concrete example of the double spending problem**
 
Abraham is owner of an [electronic coin](http://ttuesday.com/2017/08/05/transactions.html). Abraham pays Raymond for a random service with that electronic coin -- Abraham makes a copy of the existing list of transactions and marks Raymond as the new owner of the coin. Raymond verifies that it has not been forged (thanks to Abraham's [digital signature](http://ttuesday.com/2017/08/16/cryptography.html)). Raymond is now the proud owner of the electronic coin.  

Abraham decides that he also wants to buy an ebook (from Laurie this time). He no longer owns any coins. He takes the previous copy of the list of transactions (before he marked Raymond as the owner) and marks Laurie as the new owner. Laurie verifies that it has not been forged. Laurie is now the proud owner of the same coin. Problem: Abraham spent the same coin 2 times. That's called double spending, and is makes our currency not viable.

The only way for Laurie to confirm that there was no other transactions (with that coin) is for Laurie to be aware of every single transactions that ever happened. If Laurie had access to the history of that coin, she would have been able to see that Abraham had already spent the coin to pay Raymond.

**How do you make sure that everyone has access to the whole list of transactions?**

Every transactions is broadcasted to the world. Anyone can listen in (the same way they tune in a radio station) and they add each transactions to their list.

The problem with broadcasting on the Internet is that not everyone will receive messages in the same order, and we do have to ensure order otherwise Laurie might receive the coin before Raymond. The way to solve for this is to **group transactions together** and to add a timestamp to it.

Let's say group A has transaction 1, transaction 2, transaction 3 and transaction 4. The timestamp (`2017-08-23 23:11:11`) is added to that group. We take all of this information inside group A and instead of calling group A, we generate a name (called a hash), thanks to hash function[1].

Group B has transaction 5, transaction 6, a timestamp (`2017-08-23 23:21:11`) and the hash of group A.

Group C has transaction 7, transaction 8, transaction 9, a timestamp (`2017-08-23 23:31:11`) and the hash of group B.

A group of transactions is linked to the previous thanks to the hash of the previous group (which is unique based on the content of the group). In the world of Bitcoin, the groups are called blocks, and the link is call chain. We now have our concept of blockchain.

Here is a representation of it.

```
--> hash of block A  -----------------> hash of block B  -------------------------> hash of block C
    * transaction 1                     * transaction 5                             * transaction 7
    * transaction 2                     * transaction 6                             * transaction 8
    * transaction 3                     * timestamp: 2017-08-23..                   * transaction 9
    * transaction 4                     * hash of block A                           * timestamp: 2017...
    * timstamp: 2017-08-23                                                          * hash of block B
    * hash of block Z
```


One of the neat trick of in the blockchain invention is that if you want to change block A you have to change block B and block C. If you change one single character in the content of a block (the timestamp, the transaction, etc..) the hash of the block will change. If the hash changes then the reference to it from the next block will be broken. Concretely: if someone wants to alter a block from a few days ago, the link will be broken, unless that someone decides to recreate the chain of blocks starting that point.

We now have a nice blockchain (transactions grouped together and linked to the preivous one). The question you should be asking yourself is where does that blockchain live. We keep saying Laurie broadcast the transaction, but what does that actually mean? We can't use a website to host the blockchain (that would be a central authority). The solution: we let everyone host a copy of the blockchain. Instead of having one blockchain we have a many copies of the blockchain. Unfortunately, even with the timestamp solution we introduced, we can't assure that all the timestamped blocks are going to be identic if everyone is creating block based on the transaction their are receiving.

[Satoshi Nakamoto](https://en.wikipedia.org/wiki/Satoshi_Nakamoto) introduced a rule which states that we trust the blockchain that has the most computational work put into it. Computional work is a good way to get concensus on the what is the correct blockchain because it takes a lot of effort (in our case CPU cycles) to be the one that has generated the longest blockchain. CPU cycles needs electricity and electricity cost money. It would require a lot money (electricity) to fraudulently manipulate the blockchain.  

As designed above, our blocks are fairly simple to compute right now. We can almost build them by hand; a computer would barely need to work to compute them. Satoshi is actually adding articial work to build each of the block. So each of the block needs to have a **proof-of-work** which requires your computer to work very very hard in order to compute. It uses a nice little trick with cryptographic hash function that will get into next. Let's say, that the most powerful computer you ever worked with would struggle to do that work. Essentially, we need to make sure that our block looks something like this:

```
--> hash of block A  -----------------> hash of block B  -------------------------> hash of block C
    * transaction 1                     * transaction 5                             * transaction 7
    * transaction 2                     * transaction 6                             * transaction 8
    * transaction 3                     * timestamp: 2017-08-23..                   * transaction 9
    * transaction 4                     * hash of block A                           * timestamp: 2017...
    * timstamp: 2017-08-23              * proof-of-work                             * hash of block B
    * hash of block Z                                                               * proof-of-work
    * proof-of-work
```

Not everyone is actually asked to create the **proof-of-work**. Those who do are called miners (Analogy to mining gold). And the miner are actually rewarded for doing the work. They are rewarded with the same money that they are actually trying to secure. It's one of the genius of Nakamoto. It's the incentive part of bitcoin.

We now have a protocol where miners are trying to create the last block based on the transaction they received. Since they are working in parallel (also since there might be fraudsters), there will be cases when blockchains with different content will appear on the network. We agree as a group that we need always trust the blockchain that is the longest, and throw away the other chains. And this how we get to decentralize concensus on what the list of full transactions is actually accurate.

[1] A [hash function](https://en.wikipedia.org/wiki/Hash_function) is method that maps a arbitrary size data to a fixed size data.
