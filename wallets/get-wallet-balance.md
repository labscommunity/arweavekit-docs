---
description: Get the balance of an address
---

# Get Wallet Balance

The `getBalance` function returns the AR token balance in Winston (smallest possible unit of the AR token) for a given wallet address. The AR token is the native token in the Arweave ecosystem.

### Basic Syntax

The function is called as follows:

```javascript
import { getBalance } from 'arweavekit/wallet'

const address = await getBalance({params});
```

### Input Parameters

The following params are available for this function:

* `address: string` : The wallet address passed in as type `string`.
* `environment: 'local' | 'mainnet'` (optional) : The environment on which the wallet balance must be fetched.

{% hint style="info" %}
The `local` environment is configured to port <mark style="color:red;">`1984`</mark> and must have an `arlocal` instance running on the same port in the background for the function to work successfully. To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

`options` : Additional options can be passed in as a JSON object.&#x20;

* &#x20;`winstonToAr: boolean` (optional) : Set this to `true` in order to receive wallet ballance in `Ar` instead of `Winston`.

{% hint style="info" %}
**Winston** is the smallest possible unit of **AR**, similar to a [satoshi](https://en.bitcoin.it/wiki/Satoshi\_\(unit\)) in Bitcoin, or [wei](http://ethdocs.org/en/latest/ether.html#denominations) in Ethereum.

**1 AR** = 1000000000000 Winston (12 zeros) and **1 Winston** = 0.000000000001 AR.
{% endhint %}

<details>

<summary>Example</summary>

```javascript
const walletBalance = await getBalance({
    address: string,
    environment: 'local',
});
```

This returns the `AR` token balance of the entered wallet address in `Winston` for the chosen environment.

</details>

### Returned Data

The function call returns the following data:

```bash
'100000000000'
```

* `walletBalance: string` : Wallet balance in `Winston` returned as type `string` when the `winston` parameter is set to `true`.
