+++
title = "Random Numbers"
date = 2018-06-22T15:00:50+08:00
weight = 4
chapter = true
disabletoc = false
+++

# Secure Random Numbers

Getting secure random numbers is a significant challenge for blockchain smart contracts. Lity pioneers an approach to access a random number series from a seed in the current block header. The random seed is based on the hashes of all transactions in the current block, it is extremely difficult to manipulate even for the validator node that builds and proposes the block.

Inside the smart contract, you can access the random number series by simply calling the built-in function `rand()`. Below is an example.

```
pragma lity >=1.2.6;

contract RandDemo {
  uint x;
  function getRand () public returns (uint) {
    x = rand();
    return x;
  }

  function getRand2 () public pure returns (uint) {
    return rand();
  }
}
```

