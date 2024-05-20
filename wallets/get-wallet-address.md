---
description: Fetching a wallet address
---

# Get Wallet Address

The `getWallet` function returns the wallet address for a given private key.

### Basic Syntax

The function is called as follows:

```javascript
import { getAddress } from 'arweavekit/wallet'

const address = await getAddress({params});
```

### Input Parameters

The following params are available for this function:

* `key: JWKInterface` : The private key for the wallet address to be fetched. The wallet key file can be loaded as follows:

```javascript
import { readFileSync } from 'fs';

const key = JSON.parse(readFileSync('wallet.json').toString());
```

{% hint style="danger" %}
Private keys must be kept secure at all times. Please ensure that the `wallet.json` file is not pushed to a version control (eg. GitHub).
{% endhint %}

{% hint style="info" %}
It is important to `JSON.parse` the read file as this returns the `key` in the correct format (`object`) for further use.
{% endhint %}

* `environment: 'local' | 'mainnet'` : The active environment on which the wallet is interacting with.

{% hint style="info" %}
An `arlocal` instance must be running on port <mark style="color:red;">`1984`</mark> for the function to work with the local environment. To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

<details>

<summary>Example</summary>

```javascript
const walletAddress = await getAddress({
    key: { KEY_OBJECT },
    environment: 'local',
});
```

This returns the wallet address of the key entered as part of the parameters for the chosen environment.

</details>

### Returned Data

The function call returns the following data:

<pre class="language-bash"><code class="lang-bash"><strong>'WALLET_ADDRESS'
</strong></code></pre>

* `address: string` : The wallet address corresponding to the private key input is returned as type `string`.
