---
description: Introduction to smart contracts on Arweave
---

# Introduction to Smart Contracts

### Smart Contracts

A smart contract is a piece of logic stored on the blockchain. They automatically run and execute actions when certain predetermined conditions are met.

Smart contracts are deterministic. For a given set of inputs, they always return the same output, irrespective of the user. Thus, creating a trust-minimised system.

### SmartWeave Contracts on Arweave

Arweave has its own version of a smart contract system called **SmartWeave**.&#x20;

It is unique because it relies on lazy evaluation which shifts the responsibility of validating the results of the contract from the nodes to the users of the network.

The contract source code and its initial state are deployed to Arweave and posted as transactions. Then, when a user interacts with a contract, all of the prior transactions with that smart contract are evaluated until the end of chain of valid transactions. Finally, the user evaluates their latest call to the contract and writes the resulting state transition to the Arweave Network.

### Smart Contracts from a development perspective

Developers need to create user friendly tools, applications and interfaces that let users create and interact with smart contracts and associated applications for data storage, sharing, etc. on Arweave.

### Libraries used

The functions associated with smart contracts leverage the following libraries:

* [Warp SDK](https://github.com/warp-contracts/warp)

### Smart Contract based functions

In this section, we will look at the following features:

* creating a smart contract
* writing to a smart contract
* reading from a smart contract
