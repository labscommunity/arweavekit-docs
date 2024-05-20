---
description: Introduction to authentication on Arweave
---

# Introduction to Auth

### Authentication on Arweave

To interact with applications, a user must be authenticated and the application in-turn must have permissions from the user to interact with the network on the users behalf.&#x20;

Additionally, every interaction (transaction) on the network has a unique signature. The signature is a hash of the various input parameters as well as the users key that helps authenticate the transaction and point it to a particular user.

### Authentication from a development perspective

Developers need to create user friendly tools and interfaces that verify user wallet connection to applications, use wallet addressed and request permissions from users to perform actions on their behalf.

### Libraries used

The functions associated with authentication leverage the following libraries:

* [ArConnect](https://github.com/arconnectio/ArConnect)
* [Othent](https://docs.othent.io/)

{% hint style="info" %}
Currently the library only supports the ArConnect extension for compatibility reasons. Support for additional browser based wallets will be added in the future.
{% endhint %}

### Auth based functions

In this section, we will look at the following features:

* connecting a web wallet
* disconnecting a web wallet
* getting address of connected web wallet
* getting permissions from user to use connected web wallet
* getting names associated with wallet addresses
* getting all addresses from web wallet extension
* getting a users active public key from web wallet
* checking if web wallet is installed
* connecting to applications using email ids
* disconnecting email ids from applications
* fetching user details of
