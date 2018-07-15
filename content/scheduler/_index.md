+++
title = "Scheduler"
date = 2018-06-22T15:25:32+08:00
weight = 5
chapter = true
disabletoc = false
+++

### Scheduler

One of the most glaring limitations of the Ethereum platform is the lack of support for timers. Without a timer, the DApp would not be able to perform tasks such as transferring funds or executing a contract at a specified future date. That means the Ethereum smart contracts cannot easily support common real-world financial contracts such as

* Installments for e-commerce purchases
* Timeouts for various business processes that might not have definitive outcomes (eg product delivery)
* Product warranty and scheduled services
* Wills and trusts
* College or retirement savings
* Pension
* Payroll
* Stock (or coin) options
* Dividends
* Interest payments
* Insurance payments
* Mortgage payments
* And many more

That is about to change. Through engineering optimization and innovation, the CyberMiles blockchain will support timer-based transactions, including fully Ethereum-compatible fund transfers and contract executions scheduled for the future. We will also introduce a new language keyword, schedule, to support timer-based executions inside smart contracts. 

# Challenge

The lack of timer support in Ethereum is not an accident or oversight. It is due to the lack of exact time on the Proof-of-Work blockchain system. When a transaction is submitted to a blockchain, it arrives on different nodes at different times; it could be executed by different nodes at slightly different times; it could be packaged into the next block or the next 100th block by miners. Not being able to predict when (or even whether) a transaction will be executed and confirmed by miners, Ethereum does not provide a facility to trigger operations on a future time.

Therefore, on Ethereum, timer-based operations are triggered by [external off-chain computers or humans that keep time](http://www.ethereum-alarm-clock.com/). Those [time oracles](https://hackernoon.com/oracles-help-smart-contracts-resolve-subjective-events-d81639d8291c) maintain timer events and send transactions to the blockchain when tasks are due. However, the issue with the time oracles is that they are centralized entities and therefore could cheat or become unavailable at crucial moments.

There are also many efforts to create a decentralized timer system (called [alarm clock](http://www.ethereum-alarm-clock.com/)) on Ethereum. The idea is to create a cryptoeconomic game to incentivize a network of off-chain nodes to report time. We find these efforts complicated, non-scalable, and ultimately too expensive. 

> *The blockchain uncertainty principle*: the timing accuracy and cost of the of scheduled tasks are complementary variables. A short block time leads to more accurate execution time window but also more system overhead to frequently check for due tasks.

# CyberMiles support

The CyberMiles blockchain is a new generation of DPoS blockchain that features short block time and fast finality. Therefore, it is possible for validator nodes to act on scheduled tasks within the time window of a block. After the validators reach consensus on a new block, all nodes will examine the block's official timestamp and then execute tasks scheduled within the next block time from this timestamp. Since the official timestamp is created by the block proposer node, and the block is instantly final, this approach does not depend on each node's clock and hence produces deterministic outcomes on all nodes. 

We will introduce a new keyword in the Lity programming language, schedule. You can use it to schedule future fund transfers from inside a smart contract, like this.

```
schedule(transfer(), future_timestamp)
```

> CyberMiles supports a new optional transaction parameter called `scheduled_time`. When you add this parameter to any transaction, including fund transfer and smart contract execution, it will be scheduled to run in the future. Notice that this scheduled transaction will be recorded in the current block (with the current nonce), but it's execution (ie updates to the state machine) happens in the scheduled future time.

The scheduled tasks incur higher gas costs as they require more computational resources to check. The further a task is scheduled for the future, the more gas it incurs.

One of the first and simplest applications for this functionality is the "trust and will" smart contract, where you can specify to transfer your funds to another account after a certain period unless you specifically cancel. It is similar to the [Google Inactive Account Manager](https://support.google.com/accounts/answer/3036546?hl=en), but for automatic transferring of value instead of information. 

As we mentioned at the beginning of this chapter, the timer-based long running contracts represent a whole new class of smart contracts that have been proven useful in many real-world use cases. 


