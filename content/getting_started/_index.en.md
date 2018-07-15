+++
title = "Getting Started"
date = 2018-06-22T15:25:40+08:00
weight = 1
chapter = true
disabletoc = false
+++

### Getting Started

To get started, you will first need to download and install the Lity compiler. Then, write and compile a Lity smart contract. From there you can start a CyberMiles node and execute the smart contract on the blockchain.

# Download and install

Use the following link to [download the latest release of Lity](https://github.com/CyberMiles/lity/releases).
Alternatively, you can [build from the source on GitHub](http://lity.readthedocs.io/en/latest/download.html).

Extract the `lityc` program from the downloaded archive file, and place it under the user's `bin` directory.
You should be able to access it now.

```
$ which lityc
/home/username/bin/lityc
```

# A reverse Hello World

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
$ lityc --bin Reverse.lity
======= ./Reverse.lity:ReverseContract =======
Binary:
60806040526004361061004157 ...
```

Then, we also use `lityc` to generate the interface definition required 
by the virtual machine to register the contract.

```
$ lityc --abi Reverse.lity
======= ./Reverse.lity:ReverseContract =======
Contract JSON ABI
[{"constant":false,"inputs":[{"name":"input","type":"string"}],"name":"reverse","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"nonpayable","type":"function"}]
```

# Start a CyberMiles node

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

# Run the smart contract

Next, from the attached web3-cmt console, you can delpoy the smart contract and receive an address for the deployment.

```
> owner = '0x1234...'
> var bc = '60806040526004361061004157 ...'
> var abi = [...]

> var contract = web3.eth.contract(abi)
> var contractInstance = contract.new(owner, {data : bc , from : owner})
> contractInstance.address
"0xabcdCONTRACTADDRESS"
```

Then, you can call the libENI method on the deployed contract instance.

```
> contractInstance.reverse("hello", {from: owner})
olleh
```

That's it!
