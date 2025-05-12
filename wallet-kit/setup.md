---
description: Setup the Arweave Wallet Kit in React applications
---

# Setup

As seen in the introduction, the Arweave Wallet Kit utility is distributed across a few packages for modularity. The three main packages for using Arweave Wallet Kit with React apps are `@arweave-wallet-kit/core`, `@arweave-wallet-kit/react`, `@arweave-wallet-kit/styles`. The `core` and `styles` package are peer dependencies for the `react` package.

Alongside these, the strategies for each wallet have their own dedicated packages as well:

* `@arweave-wallet-kit/wander-strategy`
* `@arweave-wallet-kit/browser-wallet-strategy`
* `@arweave-wallet-kit/othent-strategy`
* `@arweave-wallet-kit/webwallet-strategy`

_Note: Othent will be deprecated by the end of 2025.  If you are integrating Arweave Wallet Kit into your dApp, it is recommended that you do NOT include the Othent strategy._ \
\
_For an Othent alternative, please check out Wander Connect:_ [_https://wander.app/connect_](https://wander.app/connect)

You can configure one or more strategies depending on the wallets you wish to add support for.

{% hint style="info" %}
Note: Currently, Arweave Wallet Kit works out of the box with ReactJS and Vite applications. Support for NextJS is in the works.
{% endhint %}

## Installation

We’ll be demonstrating the installation and setup for all 4 strategies. The Wallet Kit can be installed with any of the popular package managers as follows:

```sh
npm install @arweave-wallet-kit/core @arweave-wallet-kit/react @arweave-wallet-kit/styles @arweave-wallet-kit/wander-strategy @arweave-wallet-kit/browser-wallet-strategy @arweave-wallet-kit/othent-strategy @arweave-wallet-kit/webwallet-strategy
```

or

```sh
yarn add @arweave-wallet-kit/core @arweave-wallet-kit/react @arweave-wallet-kit/styles @arweave-wallet-kit/wander-strategy @arweave-wallet-kit/browser-wallet-strategy @arweave-wallet-kit/othent-strategy @arweave-wallet-kit/webwallet-strategy
```

or

```sh
pnpm add @arweave-wallet-kit/core @arweave-wallet-kit/react @arweave-wallet-kit/styles @arweave-wallet-kit/wander-strategy @arweave-wallet-kit/browser-wallet-strategy @arweave-wallet-kit/othent-strategy @arweave-wallet-kit/webwallet-strategy
```

or

```sh
bun install @arweave-wallet-kit/core @arweave-wallet-kit/react @arweave-wallet-kit/styles @arweave-wallet-kit/wander-strategy @arweave-wallet-kit/browser-wallet-strategy @arweave-wallet-kit/othent-strategy @arweave-wallet-kit/webwallet-strategy
```

## Setting Up the Provider

To use the library, you need to wrap your application with the Kit Provider. We’ll be using a React Vite app as an example.

```tsx
// main.tsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.tsx";
import "./index.css";
import { ArweaveWalletKit } from "@arweave-wallet-kit/react";
import WanderStrategy from "@arweave-wallet-kit/wander-strategy";
import OthentStrategy from "@arweave-wallet-kit/othent-strategy";
import BrowserWalletStrategy from "@arweave-wallet-kit/browser-wallet-strategy";
import WebWalletStrategy from "@arweave-wallet-kit/webwallet-strategy";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <ArweaveWalletKit
      config={{
        permissions: [
          "ACCESS_ADDRESS",
          "ACCESS_PUBLIC_KEY",
          "SIGN_TRANSACTION",
          "DISPATCH",
        ],
        ensurePermissions: true,
        strategies: [
          new WanderStrategy(),
          new OthentStrategy(),
          new BrowserWalletStrategy(),
          new WebWalletStrategy(),
        ],
      }}
    >
      <App />
    </ArweaveWalletKit>
  </React.StrictMode>
);
```

In the example above, the application is wrapped with the Arweave Wallet Kit Provider, passing it a `config` object as parameter with the desired wallet strategies and permissions based on the application requirements.

Once the provider is setup, you can either use the Wallet Kit’s functionality through its custom [components](connect-button.md) or [hooks](hooks.md).
