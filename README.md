# Ultimate Go: Smart Contract

Copyright 2021, 2022, Ardan Labs  
info@ardanlabs.com

## Description

This project provides material to help you learn the basics of writing, debuging, and maintaining Ethereum smart contracts. This repository has several smart contracts of increasing complexity to showcase different aspects of smart contract development. Please look at the makefile for more details and help.

## Licensing

```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

## Learn More

**Reach out about corporate training events, open enrollment live training sessions, and on-demand learning options.**

Ardan Labs (www.ardanlabs.com)  
hello@ardanlabs.com

To attend any of our high-performance tranings check out this link:  
https://www.ardanlabs.com/training  

## Installing Tooling

You must install Ethereum and Solidity into your development environment. If you are using MacOS or Linux, the makefile has brew commands to help you with this. If you can't use brew, there are links to documents in the makefile.

makefile
```
# https://geth.ethereum.org/docs/install-and-build/installing-geth
# https://docs.soliditylang.org/en/v0.8.11/installing-solidity.html

dev.setup:
	brew update
	brew list ethereum || brew install ethereum
	brew list solidity || brew install solidity
```

## Running Ethereum

Ethereum is configured to run in a developer mode that will allow for the deployment and execution of smart contracts. Use the following `make` command to start the Ethereum service. Make sure you start Ethereum in a dedicated terminal session.

```
$ make geth-up
```

To stop the Ethereum service, use the down command.

```
$ make geth-down
```

## Building Smart Contract

The smart contract can be found in `app/basic/contracts/src/store.sol` and is a smart contract written in the Ethereum programming language called Solidity. It will be helpful to install the Solidity extension by Juan Blanco. To compile and build the smart contract, run the following make command.

```
$ make basic-build
```

That will produce an `abi`, `bin`, and `go` file inside the `app/basic/contracts/store` directory. Any time code for the smart contract is changed, it must be built again for the Go applications.

## Deploying Smart Contract

With the Ethereum service up and running, run the following make command to deploy the smart contract.

```
$ make basic-deploy
```

If this is successful, the following output should be similar to.

```
go run app/basic/cmd/deploy/main.go
fromAddress: 0x6327A38415C53FFb36c11db55Ea74cc9cB4976Fd

Transaction Details
----------------------------------------------------
tx sent            : 0xafc894991575d94d1cbc004784e6d6bd4201e56fedfbe417e250f2b0a9c624ef
tx gas offer price : 0.431556798 GWei
tx gas limit       : 300000
tx value           : 0.0 GWei
tx max price       : 129467.39400000 GWei (Gas Offer Price * Max Gas Allowed)
tx max price       : 0.33014085 USD

Contract Details
----------------------------------------------------
contract id     : 0x531130464929826c57BBBF989e44085a02eeB120
export CONTRACT_ID=0x531130464929826c57BBBF989e44085a02eeB120

Waiting Logs
----------------------------------------------------
t=2022-09-07T15:58:09-0400 lvl=trce msg="Handled RPC response" reqid=2 duration=417ns

Receipt Details
----------------------------------------------------
re status          : 1
re gas used        : 299044
final cost         : 129054.471101112 GWei (Gas Offer Price * Gas Used)
final cost         : 0.32908770 USD

Balance
----------------------------------------------------
balance before     : 115792089237316195423570985008687907853269984665640564039457583061627.121056760 GWei
balance after      : 115792089237316195423570985008687907853269984665640564039457583061619.525339160 GWei
balance diff price : 7.595717600 GWei
balance diff price : 0.00001785 USD
```

Each time you deploy the contract, you will get a new contract ID. Every code change needs to be mined into a new block and therefore the API moves. Be aware what version of the API you are using.

## Executing Smart Contract API

To validate everything is working, run the follow make command.

```
$ export CONTRACT_ID=0x531130464929826c57BBBF989e44085a02eeB120
$ make basic-write
```

When you run this command, attempt to update the contracts map with the key `name` and value `brianna`. You should see the following output if everything is working correctly.

```
Input Values
----------------------------------------------------
fromAddress: 0x6327A38415C53FFb36c11db55Ea74cc9cB4976Fd
oneETHToUSD: 1571.4114863708066
oneUSDToETH: 0.0006363705551812605
contractID: 0x531130464929826c57BBBF989e44085a02eeB120
version: 1.1

Transaction Details
----------------------------------------------------
hash            : 0x270a2757da5b1e5a766dde1d3429271ca74d259c29fe0a67352859978dfcd33c
nonce           : 2
gas limit       : 250000
gas offer price : 0.896428194 GWei
value           : 0 GWei
max gas price   : 224107.0485 GWei
max gas price   : 0.35 USD

Receipt Details
----------------------------------------------------
status          : 1
gas used        : 25895
gas price       : 0.896428194 GWei
gas price       : 0.00 USD
final gas cost  : 23213.00808 GWei
final gas cost  : 0.04 USD

Logs
----------------------------------------------------

Balance
----------------------------------------------------
balance before  : 1.157920892e+68 GWei
balance after   : 1.157920892e+68 GWei
balance diff    : 17498.96476 GWei
balance diff    : 0.03 USD
```

To see if the value was written to the map for that key, run the follow make command.

```
$ export CONTRACT_ID=0x531130464929826c57BBBF989e44085a02eeB120
$ make basic-read
```

You should see the following output if everything is working correctly.

```
Input Values
----------------------------------------------------
fromAddress: 0x6327A38415C53FFb36c11db55Ea74cc9cB4976Fd
contractID: 0x531130464929826c57BBBF989e44085a02eeB120
version: 1.1

Read Value
----------------------------------------------------
value: brianna
```

## Advanced Material

[Ultimate Go: Liar's Dice](https://github.com/ardanlabs/liarsdice)  
If you are looking for more advanced and practical material, this project implements a game of Liar's Dice where a crypto wallet is used for authentication and a smart contract is used to maintain the bank. Once a player is authenticated, they bet money for each game played and that money comes from their crypto wallet.

[Ultimate Go: Advanced Engineering](https://github.com/ardanlabs/blockchain)  
This project implements a semantically correct blockchain in Go. The implementation of the Ardan blockchain takes inspiration from both Bitcoin and Ethereum. This does not incorporate any smart contract development, but is good for advanced learning.
