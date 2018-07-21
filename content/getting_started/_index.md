+++
title = "Getting started"
date = 2018-06-22T15:00:50+08:00
weight = 1
chapter = true
disabletoc = false
+++

# Getting Started

To get started, you will first need to download and install the Lity compiler. Then, write and compile a Lity smart contract. From there you can start a CyberMiles node and execute the smart contract on the blockchain.

### Download and install

To install Lity, [build from the source on GitHub](http://lity.readthedocs.io/en/latest/download.html).

Alternatively, you could [download a binary release of Lity](https://github.com/CyberMiles/lity/releases) and extract the executable `lityc` into a local
directory `~/lityc/`. 

### A reverse Hello World

The code below shows a simple Lity contract with a libENI call. 
The single libENI call costs hundreds of millions Ethereum gas to run when implemented in Solidity -- it showcases the capability of Lity and libENI.
While all Solidity smart contracts work on Lity, this example uses Lity-specific features and will not run on Solidity / Ethereum. 
First, create the text file `Reverse.lity` with the following content.
It uses a libENI extension function `reverse`, which is not available 
in standard Solidity.

```
pragma solidity ^0.4.23;
  
contract ReverseContract {
  function reverse(string input) public returns(string) {
    string memory output = eni("reverse", input);
    return output;
  }
}
```

Next, let's use `lityc` to compile the source into byte code.

```
$ ./lityc/lityc --bin Reverse.lity
======= ./Reverse.lity:ReverseContract =======
Binary:
608060405234...
```

Then, we also use `lityc` to generate the interface definition required 
by the virtual machine to register the contract.

```
$ ./lityc/lityc --abi Reverse.lity
======= ./Reverse.lity:ReverseContract =======
Contract JSON ABI
[{"constant":false,"inputs":[{"name":"input","type":"string"}],"name":"reverse","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"nonpayable","type":"function"}]
```

### Start a CyberMiles node

The Lity software we downloaded includes the `lityc` compiler and development tools.
But in order to run the smart contract, we also need the Lity virtual machine
with libENI support. You will need to run a CyberMiles blockchain node for this.

The easiest way to do this is to simply run a [Docker image for a local single node](http://travis.readthedocs.io/en/latest/getting-started.html#use-docker).
Make sure that you get to the step where you connect to the node's web3-cmt console.

Alternatively, if you are running CentOS or Ubuntu Linux distributions, you
can also [build from the source](http://travis.readthedocs.io/en/latest/getting-started.html#build-from-source).

> After you have completed the test on the local single node, you can configure 
> the node to [connect to an existing CyberMiles network](http://travis.readthedocs.io/en/latest/connect-testnet.html), and sync to become
> a full node on the blockchain. That allows your smart contracts to run on
> all nodes of the blockchain.

### Run the smart contract

Next, from the attached web3-cmt console, you can use the abi and bytecode generated from the contract above to delpoy the smart contract and receive an address for the deployment.

```
> personal.unlockAccount(cmt.accounts[0],'1234');
> bytecode="0x608060405234801561001057600080fd5b50610272806100206000396000f300608060405260043610610041576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063064767aa14610046575b600080fd5b34801561005257600080fd5b506100ad600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290505050610128565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156100ed5780820151818401526020810190506100d2565b50505050905090810190601f16801561011a5780820d805160018360200d6101000a0d1916815260200191505b509250505060405180910390f35b60608060405160206040519081016040526001905260206040519081016040527f0400000000000000000000000000000000000000000000000000000000000000905260206040519081016040526001905260206040519081016040527f04000000000000000000000000000000000000000000000000000000000000009052602060405190810160405280600090528480516020019081604051908101604052905b6020831015156101f057805182526020820191506020810190506020830392506101cb565b6001836020036101000a0d8019825116818451168082178552505050505050806040518190039052907f7265766572736500000000000000000000000000000000000000000000000000f59050809150509190505600a165627a7a723058204272fd3392dd08f71aad18d99b3593526f5b5b8859012881cab51740081dd8360029"
> abi = [{"constant":false,"inputs":[{"name":"input","type":"string"}],"name":"reverse","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"nonpayable","type":"function"}]
> contract = web3.cmt.contract(abi);
> contractInstance = contract.new(
   {
     from: web3.cmt.accounts[0],
     data: bytecode,
     gas: "4700000"
   },
   function(e, contract) {
     console.log("contract address: " + contract.address);
     console.log("transactionHash: " + contract.transactionHash);
   }
 );
```

Then, you can call the libENI method on the deployed contract instance.

```
> contractInstance.reverse.call("hello", {from: cmt.accounts[0]})
olleh
```

That's it!
