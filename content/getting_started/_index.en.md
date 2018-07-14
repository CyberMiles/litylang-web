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

# Hello World

The code below shows a simple Lity contract with a libENI call. 
The single libENI call costs hundreds of millions Ethereum gas to run when implemented in Solidity -- it showcases the capability of Lity and libENI.
While all Solidity smart contracts work on Lity, this example uses Lity-specific features and will not run on Solidity / Ethereum. 

```
TBD
```

Next, let's use `lityc` to compile the source into byte code.

```
TBD
```

# Start a local CyberMiles node

The Lity software we downloaded includes the `lityc` compiler and development tools.
But in order to run the smart contract, we also need the Lity virtual machine
with libENI support. You will need to run a CyberMiles blockchain node for this.
First, please [install docker](https://docs.docker.com/install/) on your computer.
Then, you can start the local CyberMiles node inside docker with the latest Travis build.
Let's initialize a docker image for the Travis build first.

```
$ docker run --rm -v ~/volumes/local:/travis ywonline/travis:staging node init --home /travis
```

The node's data directory is `~/volumes/local` on the local computer. Let's install libENI into it.

```
> tar zxvf $HOME/libeni.tgz -C $HOME
> mkdir -p $HOME/volumes/local/eni
> cp -r $HOME/libeni-1.2.0/lib $HOME/volumes/local/eni/lib
```

Now you can start the CyberMiles Travis node in docker.

```
$ docker run --name travis -v ~/volumes/local:/travis -t -p 26657:26657 -p 8545:8545 ywonline/travis:staging node start --home /travis
```

At this point, you can Ctrl-C to exit to the terminal and travis will remain running in the background.
You can check the CyberMiles Travis node's logs at anytime via the following docker command.

```
$ docker logs -f travis
```

You should see blocks like the following in the log.

```
INFO [07-14|07:23:05] Imported new chain segment               blocks=1 txs=0 mgas=0.000 elapsed=431.085µs mgasps=0.000 number=163 hash=05e16c…a06228
INFO [07-14|07:23:15] Imported new chain segment               blocks=1 txs=0 mgas=0.000 elapsed=461.465µs mgasps=0.000 number=164 hash=933b97…0c340c
```

# Run the smart contract

You can connect to the local CyberMiles node by attaching an instance of
the Travis client.

```
# Get the IP address of the travis node
$ docker inspect -f '{{ .NetworkSettings.IPAddress }}' travis
172.17.0.2

# Use the IP address from above to connect
docker run --rm -it ywonline/travis:staging attach http://172.17.0.2:8545
```

It opens the web3-cmt JavaScript console to interact with the virtual machine.
The example below shows how to deploy the bytecode from `lityc` to the virtual machine as a smart contract.

```
Welcome to the Travis JavaScript console!

instance: vm/v1.6.7-stable/linux-amd64/go1.9.3
coinbase: 0x7eff122b94897ea5b0e2a9abf47b86337fafebdc
at block: 231 (Sat, 14 Jul 2018 07:34:25 UTC)
 datadir: /travis
 modules: admin:1.0 cmt:1.0 eth:1.0 net:1.0 personal:1.0 rpc:1.0 web3:1.0

> personal.unlockAccount('0x7eff122b94897ea5b0e2a9abf47b86337fafebdc', '1234')
true
> 
```

And finally, let's execute a method on the smart contract.


