+++
title = "Performance"
date = 2018-06-22T15:25:25+08:00
weight = 2
chapter = true
disabletoc = false
+++

### Performance

The Lity virtual machine supports heavy optimization for specific computing
tasks by extending the virtual machine runtime using 
C++ or other high performance native techniques.
This approach is called Ethereum Native Interface (ENI): [libENI](http://libeni.readthedocs.io/en/latest/).

On the CyberMiles blockchain, we provide libENI functions optimized for
common e-commerce scenarios, such as PKI-based encrytion to protect privacy.
But as a general virtual machine technology, libENI can be utilized to
optimize many different kinds of blockchain virtual machines.

> For instance, using Ethereum smart contract to verify header of 
> a single bitcoin transaction (i.e., a scrypt operation) will cost 370M 
> Ethereum gas, which is more than 1 Billion Gwei (1 ETH) at the gas price 
> of 3 Gwei. And it has to be done across multiple 
> Ethereum blocks to avoid exceeding the block gas limit.
> In libENI, the entire scrypt operation can be completed with one function call.
> It takes milli-seconds and consumes a few pennies of gas fees.
> You can [learn more here]().

# Use

TBD

# Develop

The [libENI developer guide](http://libeni.readthedocs.io/en/latest/developer-guide.html) discusses how to create new  

# Governance

TBD
