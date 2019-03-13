---
title: "Litylang"
---

# What is Lity

Lity is a new programming language for building blockchain smart contracts. It consists of a *dynamically extensible language*, a *compiler*, and a *virtual machine* on the CyberMiles blockchain. It is a superset of the Solidity language and is more extensible, performant, and safe. Specifically,

* The [libENI](https://www.litylang.org/performance/) dynamic VM extension allows native functions to be added to the virtual machine on the fly, without stopping, forking or upgrading the blockchain. 

* Lity language's built-in function `isValidator` allows smart contracts to check whether the transaction sender is a current validator of the underlying blockchain (supported on DPoS blockchains such as CyberMiles). Through the `ValidatorOnly` modifier, we can create ["trusted" smart contract methods](https://www.litylang.org/trusted/) that can only be executed by validators. A common use case of such trusted smart contracts is for them to serve as oracles to provide off-chain and cross-chain states.

* Lity language's built-in function `rand` allows smart contracts to get [highly secure random numbers](https://www.litylang.org/rand/). The random seed is generated from the underlying consensus mechanism and is further secured by the DPoS validators.

* The [Lity Rules Engine](https://www.litylang.org/business_rules/) allows formal business rules to be embedded in smart contracts. The rules engine evaluates and executes the rules automatically. That could drastically increase developer productivity and reduce errors.

* The Lity language [prevents integer overflow errors](https://www.litylang.org/security/#overflow-protection). It introduces a new number type called `safeuint`. It is an unsigned integer (`uint`) but all `safeuint` operations are automatically wrapped in SafetMath functions. Furthermore, the CyberMiles Virtual Machine (CVM) detects and stops integer overflows at runtime. The use of `safeuint` and CVM eliminates a large class of smart contract errors that resulted in significant fund loss in the past.

* The Lity language supports [fixed point real numbers](https://www.litylang.org/number/), as opposed to integer-only arithmetics in Solidity.

* Lity smart contracts [support alternative gas mechanisms](https://www.litylang.org/gas/). For example, a contract could designate some functions to be `freegas` and the gas fees for these functions will be deducted from the contract owner's address allowing them to be used free of charge by end users.

* The Lity compiler provides tooling for security and error checks before the Lity smart contract is deployed. The [ERC checker](https://www.litylang.org/security/#erc-checker) in the Lity compiler analyzes the source code and automatically checks if the contract conforms to known ERC standards. The compiler also integrates with the [Oyente static analyzer](https://www.litylang.org/security/#static-analysis) to detect common error patterns from the compiled bytecode.

* Lity language's built-in function `schedule` allows smart contracts to [schedule timer tasks](https://www.litylang.org/scheduler/) to be executed in the future, which is required by many real-world business contracts such as trust, will, installment payments, insurance, stock options, and investment returns.

Still interested? [Get started here!](https://www.litylang.org/getting_started/)

The name Lity pays homeage to to Solidity, and inspires to be more flexible / expansible (liquid) and more performant (combustable) at the same time. Lity is developed by the Second State Inc in collaboration with the [CyberMiles Foundation](https://www.cybermiles.io/), and is released under GPL as Free Software. All rights reserved.
