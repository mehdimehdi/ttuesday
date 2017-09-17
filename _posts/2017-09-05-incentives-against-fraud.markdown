---
layout: post
title:  "Incentives against fraud"
date:   2017-09-05 01:05:41 -0700
---

The electronic cash created is valuable only if we solve for [double spending](/2017/08/28/double-spending.html). The blockchain is the solution to prevent double spending and thus ensure the currency has value. The genius of Nakamoto, is to reward the miners doing all the hardwork of securing the blockchain with the same electronic cash they help securing. It's a self-contained solution, it does not add dependencies to any other systems.

Miners are mining blocks. Mining is cute metaphor (comparison with mining gold) for creating the proof-of-work. And the reason why the "mining" metaphor works so well is because for every block successfully mined, 1/ the miner gets rewarded with electronic cash, 2/ new coins are introduced in the circulation. Instead of needing a central authority that gets paid to keep your bank account secure, anyone with computing power in the world and connected to the internet can get rewarded for helping keeping the system secured.

At the top of a new block (`header`) the miner is allowed to create a new digital coin (the block reward) and make himself the owner of that coin.

There is a limited number of coins that will ever be issued (21 million bitcoins by 2140). Introducing new coins via the block reward helps distributing coins in the system. This makes the currency itself inflationary until 2140, then deflationary because people will inevitably lose their [public or private key](/2017/08/16/cryptography.html).

This is why there is also another type of reward for theminer: the transaction fee. The miners get rewarded with the new coin created and the transaction fee. Both values change over time based how close we are to the 21 million coins in circulation and on the fee market (cf. below). The people transacting pay for the fee to get their transactions added to the blockchain (or not).

The amount of work required to compute the proof-of-work is configurable so that it matches the pace of creating a new block every 10 minutes. If there are a lot of miners trying to solve the really hard problem, by default the probability of solving it faster is higher, so the algorithm self configures to make the problem harder. If there is almost no-one in the network trying to solve the hard problem then the probability of finding a solution in 10 minutes is actuallly harder so the algorithm configures itself to be easier.

**Potential frauds**

Anyone interested in assembling enough computing power to attack the system is better off working towards making the system actually work because the cost/reward ratio is in favor of being honest. It would cost a lot of money (more than 50% of the total computing power participating) to potentially defraud people. It actually earns money to help run the system smoothly. The incentives are aligned to help run an honest system as it earns more money.

**Controlled reward structure and market**

In a centralized economy, the currency is generated at a rate that is planned by a central bank. It attempts to match the growth of the amount of goods that are exchanged in the said economy. In our decentralized monetary system, the supply is controlled by the algorithm ran accross each participant of the network. The block reward value has been set to decrease by 50% every 4 years. It is how the supply of bitcoin is controlled.

The most innovative systems mix two seemingly orthogonal concepts into a perfectly coherent ecosystem. Decentralization and market economy make a perfect combination for digital currencies. The decentralization brings protection against illegitamicy of a once trusted third party. Market economy provides efficiency to keep the system running at the lowest maintainable cost possible.

As the currency development stablizes and usage increases, the incentives (mining reward and transactions) will self-regulate via supply & demand. The demand being the people wanting get their transactions on the blockchain, and willing to pay certain price (fees) for it. And the supply being the miner wanting to gain the block reward and the fee. The block reward value is slowly decreasing and the proof-of-work is more or less hard to compute depending on the number of people trying to solve it. On the other side, the transaction fee looks more like a pure market. The people transacting who want priority to get on the blockchain will pay a higher fee to get prioritized, and the people that don't pay will be added to the blockchain at a later date.

If we want to think at of our peer-to-peer electronic cash not only as a store of value, but also as a medium of exchange, this means that there is an opportunity to augment the current bitcoin protocol. And this need is not staying unanswered.
