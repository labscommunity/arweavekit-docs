---
description: React hooks that provide deeper access into the wallet APIs
---

# Hooks

Inside the [`<ArweaveWalletKit>`](setup.md#setup-provider), you can use all kinds of hooks that are reactive to the different [strategies](./#terminology). Some of the hooks and/or api functions might not be supported by all wallets.

## `useConnection`

The core hook for connecting / disconnecting a [strategy](./#terminology).

**Usage**

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

API hook. Returns the active [strategy](./#terminology)'s API as an intractable object. Can be used to sign/encrypt, etc.

**Usage**

```ts
const api = useApi();

// sign
await api.sign(transaction);

// encrypt
await api.encrypt(...)
```

{% hint style="warning" %}
Some API functions might not be supported depending on the strategy the user chose. (e.g.: Othent does not support the `signature()` function.
{% endhint %}

## `useProfileModal`

Toggle / display a modal with profile information and a disconnect button.

```ts
const profileModal = useProfileModal();

profileModal.setOpen(true);
```

## `useActiveAddress`

Active address hook. Requires the [`ACCESS_ADDRESS`](https://docs.arconnect.io/api/connect#permissions) and the [`ACCESS_ALL_ADDRESSES`](https://docs.arconnect.io/api/connect#permissions) permission.

**Usage**

```ts
const address = useActiveAddress();
```

## `usePublicKey`

Active address hook. Requires the [`ACCESS_PUBLIC_KEY`](https://docs.arconnect.io/api/connect#permissions) permission.

**Usage**

```ts
const publicKey = usePublicKey();
```

## `usePermissions`

Permissions hook. Returns the permissions given to the app, known by Arweave Wallet Kit.

**Usage**

```ts
const permissions = usePermissions();
```

## `useAddresses`

All addresses hook. Returns the addresses in the connected wallet, known by Arweave Wallet Kit. Requires the [`ACCESS_ALL_ADDRESSES`](https://docs.arconnect.io/api/connect#permissions) permission.

**Usage**

```ts
const addresses = useAddresses();
```

## `useWalletNames`

All addresses hook. Returns the addresses in the connected wallet, known by Arweave Wallet Kit. Requires the [`ACCESS_ALL_ADDRESSES`](https://docs.arconnect.io/api/connect#permissions) permission.

**Usage**

```ts
const walletNames = useWalletNames();
```

## `useStrategy`

Active [strategy](./) hook. Returns the currently used strategy's ID (["arconnect"](https://arconnect.io), [`"webwallet"`](https://arweave.app), etc.)

**Usage**

```ts
const strategy = useStrategy();
```
