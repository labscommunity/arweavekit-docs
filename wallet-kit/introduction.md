---
description: Hooks and Components for unified interaction with Arweave wallets
---

# Introduction to Arweave Wallet Kit

<figure><img src="../.gitbook/assets/Arweave Wallet Kit - Wander.png" alt=""><figcaption></figcaption></figure>

The Arweave Wallet Kit simplifies interactions between Arweave wallets and dApps, offering a unified API that supports any Arweave wallet. Users can easily interact with apps using their preferred wallet.

The Kit is divided into multiple packages for modularity and extensibility:

* A core package that is foundation for all functionality.
* A set of React hooks and components built on the core package.
* A styles package that complements the React hooks and components.

Support for other frameworks can be developed using the core package.

The support for various wallets is modular as well. It is broken down into “strategies”, with each having its own package.

## Terminology

In Arweave Wallet Kit, a _strategy_ is an implementation of an Arweave wallet within the kit. These strategies allow the user to communicate with all wallets in a standard way and with a common API.

## Supported wallets

The library currently supports the following wallets:

* [Wander.app](https://www.wander.app)
* [Arweave.app](https://arweave.app)
* [Othent](https://othent.io/)
* General Browser Wallets
