---
layout: post
title:  "Incentives against fraud"
date:   2017-09-05 01:05:41 -0700
---

The electronic cash created is valuable only if we solve for double spending. The secured blockchain is the solution to prevent double spending and thus ensure the currency has value. The genius of Nakamoto, is to reward the miners doing all the hardwork of securing the blockchain with the own electronic cash they are helping to secure. It's a self-contained solution.

We now have miner, mining blocks. Mining is cute metaphor (comparison with mining gold) for creating the proof-of-work. And the reason why the "mining" metaphor works so well is because for every block successfully mined, the miner gets rewarded with electronic cash. Instead of needing a central authority to ge rewarded for keeping your bank account secure, anyone in the world with computing power can potentially get rewarded for helping keeping the system secured.

Here is how a miner gets rewarded for having built the proof-of-work. At the top of the block just mined (the `header`) the miner is allowed to create a new digital coin and make himself the owner of that coin:

> This adds an incentive for nodes to support the network, and provides a way to initially distribute coins into circulation, since there is no central authority to issue them
>> Satoshi Nakamoto (Original bitcoin paper)

**How many digital coin should the miner be rewarded?**

This is yet another genius invention of Nakamoto. The miner will be rewarded at least more coin that the amount of money required to compute the proof-of-work, and if that amount is smaller than the cost to process the proof-of-work, then the reward will be padded with a transaction fee.

There is a limited number of coins that will ever be issued (21 million bitcoins by 2140). Introducing new coins helps distributing coins in the system (the same way gold miners were expanding resoruces) but there is a known limit to the coins added. This makes the currency itself inflationary until 2140, then deflationary because people will inevitably lose their [public or private key]().

So now, we haven't gone into a lot of details about the what's is required to create the proof-of-work, but whithout getting into to much details, we can describe that the amount of work required is actually configurable so that it matches the pace of creating a new block every 10 minutes. If there are a lot of miners try to solve the really hard problem, by default the probably of solving it faster is higher, so the algorithm self configures to make the problem harder. If there is almost no-one in the network to solve the hard problem then the probably of finding a solution in 10 minutes is actuallly harder so the algorithm configures itself to be easier.
