+++
title = "Performance"
date = 2018-06-22T15:25:25+08:00
weight = 2
chapter = true
disabletoc = false
+++

# Performance

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
> You can [learn more here](http://lity.readthedocs.io/en/latest/verify-dogecoin-block-on-travis.html).

### Use

An increasing number of libENI functions are already integrated into the 
Travis software and the CyberMiles blockchain network. To use them in your 
smart contarct is to simply use the `eni` keyword together with the libENI
function name and function parameters. For example, the `scrypt` function
works like the following. It takes the `block_header_hex` from a Dogecoin block
as the input paremeter.

```
contract DogecoinVerifier {
  function verifyBlock(uint version, string prev_block, string merkle_root, uint timestamp, string bits, uint nouce) pure public returns (bool) {
    DogecoinBlockHeader memory block_header = DogecoinBlockHeader(version, prev_block, merkle_root, timestamp, bits, nouce);
    string memory block_header_hex = generateBlockHeader(block_header);
    string memory pow_hash = reverseHex(eni("scrypt", block_header_hex));
    uint256 target = bitsToTarget(bits);
    if (hexToUint(pow_hash) > target) {
      return false;
    }
    return true;
  }
  ...
}
```

### Develop

To develop a new libENI function, you will need two things:

1. To implement the function in native C++.
2. To implement how to compute gas fees for this function.
3. To build the function into a shared library file.
4. To deploy this library file so that the virtual machine can find it when executing the contracts. 

Notice that we only need to copy the shared library to a file location where
the virtual machine can find it. There is no change to the virtual machine
itself. That allows new libENI functions to be dynamically deployed (and removed)
without any change to the rest of the system. That is an especially desirable 
feature for blockchains where we cannot stop and restart to deploy new features.

For more details, please refer to the
[libENI developer guide](http://libeni.readthedocs.io/en/latest/developer-guide.html).

### Governance

While anyone can create a new libENI function, all public blockchains have 
governance structures to determine which functions should be made available
on the blockchain. In the case of the CyberMiles blockchain, validators make
this decision. 

Validators use [governance transactions](http://travis.readthedocs.io/en/latest/governance.html) to propose new libENI functions,
and vote to accept them. Once a libENI function is accepted, all nodes will
process the governance transaction and download the shared library to
the local appropriate data directory.
 
