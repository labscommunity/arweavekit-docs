---
description: React hooks that provide deeper access into the wallet APIs
---

# Hooks

Inside the [`<ArweaveWalletKit>`](setup.md#setup-provider), you can use all kinds of hooks that are reactive to the different [strategies](introduction.md#terminology). Some of the hooks and/or api functions might not be supported by all wallets.

## `useConnection`

This is the core hook for connecting / disconnecting a [strategy](introduction.md#terminology).

To use the different functionalities the various Arweave wallets provide, you need to request permissions from the user to interact with their wallets. This can be done with the `connect()` function.

To end the current Wander session for the user, you can disconnect from the extension, using the `disconnect()` function. This removes all permissions from your application.

The `connected` function is simply a boolean for checking whether the user is connected with the application.

### Usage

```ts
const { connected, connect, disconnect } = useConnection();

// initiate connection
await connect();

// disconnect the connected strategy
await disconnect();

// is there a strategy connected?
connected ? "wallet connected" : "no connected wallet";
```

## `useApi`

The API hook returns the active [strategy](introduction.md#terminology)'s API as an intractable object. Can be used to sign/encrypt, etc.

### Usage

```ts
const api = useApi();

// sign
await api.sign(transaction);

// encrypt
await api.encrypt(...)
```

{% hint style="warning" %}
The available API functions may vary depending on the chosen strategy.
{% endhint %}

## `useProfileModal`

Toggle visibility (display/ hide) a modal with the connected user’s profile information and a disconnect button.

```ts
const profileModal = useProfileModal();

profileModal.setOpen(true);
```

## `useActiveAddress`

The Active address hook returns the address that is currently connected with the application. It requires the [`ACCESS_ADDRESS`](https://docs.wander.app/api/connect#permissions) and the [`ACCESS_ALL_ADDRESSES`](https://docs.wander.app/api/connect#permissions) permission.

### Usage

```ts
const address = useActiveAddress();
```

## `usePublicKey`

The Active address hook returns the public key that is currently connected with the application. It requires the [`ACCESS_PUBLIC_KEY`](https://docs.wander.app/api/connect#permissions) permission.

### Usage

```ts
const publicKey = usePublicKey();
```

## `usePermissions`

The Permissions hook returns the permissions given to the application by the connected user.

### Usage

```ts
const permissions = usePermissions();
```

## `useAddresses`

This hook returns all the addresses in the connected wallet, known by Arweave Wallet Kit. This is useful for fetching all the addresses a connected user may have. It requires the [`ACCESS_ALL_ADDRESSES`](https://docs.wander.app/api/connect#permissions) permission.

### Usage

```ts
const addresses = useAddresses();
```

## `useWalletNames`

This hook returns any names associated with all the addresses the connected user may have. An example of these names are ANS names that can be associated with any Arweave wallet addresses. It requires the [`ACCESS_ALL_ADDRESSES`](https://docs.wander.app/api/connect#permissions) permission.

### Usage

```ts
const walletNames = useWalletNames();
```

## `useStrategy`

Active [strategy](introduction.md#terminology) hook. Returns the currently used strategy's ID ([`"wander"`](https://www.wander.app/), [`"webwallet"`](https://arweave.app), etc.)

### Usage

```ts
const strategy = useStrategy();
```
