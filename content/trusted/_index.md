+++
title = "Trusted Smart Contracts"
date = 2018-06-22T15:00:50+08:00
weight = 3
chapter = true
disabletoc = false
+++

# Trusted Smart Contracts

One of the most important services on blockchains is the oracle service. An oracle is typically a smart contract that makes external data (i.e., off chain, real world, or cross chain) determinstically available on the blockchain. It provides a single source of truth for off chain states, and hence allows blockchain nodes to reach consensus.

The traditional oracle is highly centralized and goes against the spirit of the decentralized blockchain. For example, a delivery service oracle that provides delivery status of packages might be established by Fedex. A weather oracle might be established by a weather station. In order to use those oracles, blockchain users and DApps must trust the entities behind those oracles.

A second approach for oracles is to create a community-based cryptoeconomic game for members of the community to compete and provide the truth in a smart contract. Examples of such oracles include the [BTC Relay](http://btcrelay.org/) to provide information about the Bitcoin blockchain, and the [Ethereum Alarm Clock](https://www.ethereum-alarm-clock.com/) to provide time.

In Lity, however, we take a different approach to create trusted smart contracts, and make oracles first class citizens on the CyberMiles blockchain. On the CyberMiles blockchain, the DPoS validators (super nodes) are trusted entities. They must stake a large amount of tokens from your own account and from their supporters / community. Those tokens are subject to slashing and confiscation if the validator misbehaves. So, if a smart contract can only be updated by current validators, data from this contract should have a high level of trust on the CyberMiles blockchain.

In the Lity language, we provide a built-in function called `isValidator` to check whether the current transaction sender / function caller is a validator. Then with the `ValidatorOnly` modifier, we can construct smart contracts that act as trusted oracles on the blockchain. [See more here](https://lity.readthedocs.io/en/latest/validator-only-contract.html#validator-only-contract).
