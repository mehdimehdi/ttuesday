---
layout: post
title:  "Cryptography applied to elecronic cash"
date:   2017-08-16 18:00:00 -0700
---

In order to build a peer-to-peer electronic cash system, we can't rely on a central trusted third party (It wouldn't really be peer-to-peer otherwise). One of the major service[1] a central trusted third party provides is to verify identities when one wants to transact.

Let's take the example of Venmo. Venmo is a central trusted third-party. If Laurie sends money to Raymond through the Venmo application. Venmo handles the identification and authentication (phone number + password, email + password or Touch ID, etc.). Venmo validates the identities of Laurie (to send the money) and Raymond (to receive the money).

In [Nakamoto](https://en.wikipedia.org/wiki/Satoshi_Nakamoto)'s quest to build an eletronic peer-to-peer cash system, he hoped to avoid by-pass a trusted third-party.[2]

Without a trusted third-party, we are be forced to trust no-one. We still want to transact though. So here is the trick: we make all the transactions available to everyone: completely public. Anyone interested in looking at the electronic transactions can look at them, copy them. Everyone knows who's buying from who (transacting). The person who's initiating the transaction makes the transaction public to anyone that has an internet connection.

So now, we have a list of transactions (electronic cash) with Raymond's name on it (because he is the last owner). Raymond is the owner of the electronic cash. It has value to Raymond. It probably has value to someone else too. The main problem is: what stops Raymond's nemesis (Abraham), from copying that list of transactions, adding another transaction at the end of the list that claims that he is the new owner? If Abraham does this, and publishes back on the internet, at this point Abraham would have stolen the electronic cash from Raymond! No one would want to use a cash system that could so easily be robbed.

Public key cryptography is a sub-field of cryptography that provides a solution to this problem. It provides a mathematical mechanism to validate that the transaction was agreed upon with no way for Abraham to fake a transaction.

What we are concretely trying to do is verify that a transaction (Laurie sends money to Raymond) was allowed by Laurie, and provide the assurance that Laurie can't deny that she allowed it.

The mathematics behind digital signature is pretty complex and there are [great resources](https://www.youtube.com/watch?v=YEBfamv-_do) that get in the details of it.

Laurie needs to create a public key and a private key. The public key is what identifies Laurie, and what is provided in order to receive a transaction. (Laurie doesn't actually give her name --it's also useful for anonimity[3]--). The private key is something that you keep very secure and you don't share with everyone. Treat even more carefully than a password, because you can't change it.

Laurie has:
 1. Public key
 2. Private key
 3. Public key of Raymond (who's suppose to receive the electronic cash)

Laurie uses a mathematical method to generate a string of characters based on all of these information: it's called "signing", and it generates the what's called the signature.

Anyone in the network has:
 1. Laurie's public key.
 2. Raymond's public key (the new owner).
 3. The signature.

There is an easy way (mathematical method) to look at the signature and confirm that it was actually signed by Laurie, and no-one else. This also assures that Laurie signed it. She can't claim she didn't do it because only someone with Laurie's private key could have generated that signature.

If you like to think in analogies, here is how you need to think about it: the signature is a wax seal on an envelope. Anyone can open the envelope and look at the content, but the presence of the seal proves that the content was added in the envelope by the sender.

Now what we used to have trusted third parties to help us ensure the identities of everyone involved in a transaction. We applied cryptography to ensure identities wihtout the need of third-parties.
Third-parties also provide a solution against [double spending](http://ttuesday.com/2017/08/28/double-spending.html) which is important to solve to have usable electronic cash system. Interestingly enough, cryptography also provides a solution to the 'double spending' problem. We will cover it next.

[1] Double spending is another really important benefit that I'll discuss in a future post.  
[2] Removing a trusted third-party is important and fascinating for a lot of reason that I won't discuss in this piece. Bear with me: just assume that it is for the better, at least for the sake of this discussion.  
[3] Anonmininty is another property of cash tha tis pretty cool and that I will eventually discuss.  
