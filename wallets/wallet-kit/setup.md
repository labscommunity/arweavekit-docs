---
description: Setup the Arweave Wallet Kit component library
---

# Setup

## Installation

The Wallet Kit is available on [npm](https://www.npmjs.com/package/arweave-wallet-kit).

```sh
yarn add arweave-wallet-kit
```

or

```sh
npm i arweave-wallet-kit
```

## Setup provider

To use the library, you'll need to wrap your application with the Kit Provider.

```tsx
import { ArweaveWalletKit } from "arweave-wallet-kit";

const App = () => {
  return (
    <ArweaveWalletKit>
      <YourApp />
    </ArweaveWalletKit>
  );
};
```
