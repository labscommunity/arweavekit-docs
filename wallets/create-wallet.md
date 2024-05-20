---
description: Creating an Arweave wallet
---

# Create Wallet

The `createWallet` function creates a new wallet capable of interacting with Arweave and Arweave based applications.

{% hint style="info" %}
The created wallet does not have any tokens or assets in it. For transactions, the wallet may need to be supplied with funds.
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { createWallet } from 'arweavekit/wallet'

const wallet = await createWallet({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `seedPhrase: boolean` (optional) : Returns the seed phrase of the newly created wallet if set to `true`.
* `environment: 'local' | 'mainnet'` (optional) : The environment for creating the wallet. The wallet created is funded with `1000000000000 Winston` for the `local` environment. Wallets created on the `mainnet` need to be funded separately.

{% hint style="info" %}
An `arlocal` instance must be running on port <mark style="color:red;">`1984`</mark> for the function to work with the `local` environment. And any funds in the wallet will be available only as long as the same instance of `arlocal` is running.  To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

{% hint style="info" %}
**Winston** is the smallest possible unit of **AR**, similar to a [satoshi](https://en.bitcoin.it/wiki/Satoshi\_\(unit\)) in Bitcoin, or [wei](http://ethdocs.org/en/latest/ether.html#denominations) in Ethereum.

**1 AR** = 1000000000000 Winston (12 zeros) and **1 Winston** = 0.000000000001 AR.
{% endhint %}

<details>

<summary>Example</summary>

```javascript
const wallet = await createWallet({
    seedPhrase: true,
    environment: 'local',
});
```

This creates a new wallet on the local network that is pre-funded with `1000000000000 Winston (1 AR)` and returns the seedPhrase for the same along with the private key and wallet address.

</details>

### Returned Data

The function call returns the following data:

```bash
{
key: { KEY_OBJECT },
walletAddress: 'WALLET_ADDRESS',
seedPhrase: '12_WORD_SEED_PHRASE'
}
```

* `key: JWKInterface` : The private key is a JSON object. Read more about the Arweave compatible key format [here](https://docs.arweave.org/developers/server/http-api#key-format).

{% hint style="danger" %}
The key provides access to a wallet and any assets associated with it. It is crucial to keep the key secure and not publish it anywhere.
{% endhint %}

{% hint style="info" %}
Store the value of `key` in a file with the `.json` extension for later use.
{% endhint %}

* `walletAddress: string`: The wallet address is derived from the public key by truncating it down to 43 characters.
* `seedPhrase: string` (optional) : This is a 12 word `string` that can be used to recover a wallet and any assets associated with it.

{% hint style="danger" %}
It is is crucial to keep the seed phrase secure and not publish it anywhere.
{% endhint %}

{% hint style="info" %}
The seed phrase is returned only if the input parameter is set to true.
{% endhint %}
