+++
title = "Security"
date = 2018-06-22T15:00:50+08:00
weight = 3
chapter = true
disabletoc = false
+++

# Security

A key innovation of the Lity compiler and virtual machine is that
they are proactive in preventing common smart contract security
issues. We have categorized known security issues with Ethereum
Solidity smart contracts, extracted common coding patterns that lead to
those issues, and installed checks for those patterns in both the Lity
language compiler and the virtual machine. We believe that 95% of
smart contract bugs that lead to money loss on Ethereum will not 
occur in the first place on the CyberMiles blockchain.

### ERC checker

The ERC checker is a Lity compiler facility to make sure that smart contracts
correctly complies to the ERC standards they claim to implement.

* [ERC20](https://theethereum.wiki/w/index.php/ERC20_Token_Standard) is the most common token / coin issuance contract standard. [See ERC20 checker in action](http://lity.readthedocs.io/en/latest/erc-contract-standard-checker/erc20-checker.html#erc20-contract-standard-checker).
* [ERC223](https://github.com/ethereum/EIPs/issues/223) is an enhancement to ERC20. It guards against inadvertent fund transfers to contract addresses, which is a common source of fund loss on Ethereum. We recommend that all ERC20 contracts on CyberMiles conform to the ERC223 standard for better safety. [See ERC223 checker in action](http://lity.readthedocs.io/en/latest/erc-contract-standard-checker/erc223-checker.html#erc223-contract-standard-checker).
* [ERC721](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md) is the contract standard to issue non-fungible tokens. [See ERC721 checker in action](http://lity.readthedocs.io/en/latest/erc-contract-standard-checker/erc721-checker.html#erc721-contract-standard-checker).
* [ERC827](https://github.com/ethereum/EIPs/issues/827) is another enhancement to make ERC20 easier and safer to use while maintaining compatibility with ERC20 tools. [See ERC827 checker in action](http://lity.readthedocs.io/en/latest/erc-contract-standard-checker/erc827-checker.html#erc827-contract-standard-checker).
* [ERC884](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-884.md) is a security token standard to issue stick certificates. [See ERC884 checker in action](http://lity.readthedocs.io/en/latest/erc-contract-standard-checker/erc884-checker.html#erc884-contract-standard-checker).

### Overflow protection

One of the most common security issues in Ethereum smart contracts is 
[integer overflow](https://medium.com/cybermiles/building-a-safer-crypto-token-27c96a7e78fd). Lity proactively eliminates the opportunities for integer overflow
in smart contract code. Specifically,

* The Lity compiler checks for the use of SafeMath on integers. It throws warnings if integer operations are not wrapped around in SafetMath.
* The CyberMiles Virtual Machine detects integer overflow at runtime, and stops the contract execution with an error, as opposed to continuing with the
overflen integer numbers.

