+++
title = "Gas Discounts"
date = 2018-06-22T15:00:50+08:00
weight = 8
chapter = true
disabletoc = false
+++

# Gas Discounts

One of the major issues with public blockchains is the "one size fits all" pricing scheme for transaction costs (gas fees).
It makes the blockchain service too expensive for many use cases, since the gas price is determined by the use cases
that are willing to pay the most.

Application specific blockchains, such as the CyberMiles blockchain for e-commerce applications, can alleviate this problem.
Yet still, within the e-commerce space, financial applications are probably much less sensitive to infrastructure costs than
dispute resolution applications.

To resolve this problem, the blockchain should provide a governance strategy to set different gas prices for 
different smart contracts. On CyberMiles, the [governance transactions](https://travis.readthedocs.io/en/latest/governance.html) 
allow smart contract creators to apply for discounted gas
prices, and the discounts could be approved by a vote by CyberMiles validators. Once approved, the CyberMiles Virtual
Machine will apply the discount to gas computations for the contract. That allows validators to promote certain
types of applications on the CyberMiles blockchain and forester a healthy ecosystem.

