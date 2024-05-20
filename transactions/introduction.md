---
description: Introduction to transactions on Arweave
---

# Introduction to Transactions

### Transactions on Arweave

Any change to the state of the blockchain (information stored on chain) is considered a transaction.

The two common types of transactions on Arweave are uploading data on chain and transfer of assets between wallets.

The transaction process on Arweave is split into 3 steps for convenience,  customisation and reduction in compute time. Namely, creating the transaction, signing it and then posting it on Arweave. The next pages look at these in depth.

### Transactions from a development perspective

Developers need to create user friendly tools, applications and interfaces that let users perform transactions like uploading data on chain or sending tokens without the need for writing code for it.

### Libraries used

The functions associated with transactions leverage the following libraries:

* [Arweave JS](https://github.com/ArweaveTeam/arweave-js)
* [Bundlr Network SDK](https://docs.bundlr.network/category/basic-features)
* [Othent](https://othent.io/)

### Transaction based functions

In this section, we will look at the following features:

* creating a transaction
* signing a transaction
* posting the transaction on chain
* getting the status of a transaction
* getting an existing transaction from the network
* creating and posting a transaction to the network with Othent

