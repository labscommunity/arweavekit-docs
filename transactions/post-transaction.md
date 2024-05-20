---
description: Post a signed transaction on Arweave
---

# Post Transaction

This is the final step of the transaction process on Arweave.

The `postTransaction` function uploads the previously signed transaction on Arweave.

### Basic Syntax

The function is called as follows:

```javascript
import { postTransaction } from 'arweavekit/transaction'

const postedTransaction = await postTransaction({params}) 
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `key: JWKInterface` (optional): The private key for the wallet posting the transaction. The wallet key file can be loaded as follows:

```javascript
import { readFileSync } from 'fs';

const key = JSON.parse(readFileSync('wallet.json').toString());
```

{% hint style="info" %}
Make sure to use the same private key used in the `signTransaction` function.
{% endhint %}

* `environment: 'local' | 'mainnet'` (optional) : The environment on which the transaction was created and signed.

{% hint style="info" %}
An `arlocal` instance must be running on port <mark style="color:red;">`1984`</mark> for the function to work with the local environment. To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

* `transaction: object` : The transaction object signed previously.

<details>

<summary>Example</summary>

```javascript
const postedTransaction = await postTransaction({
    transaction: transaction,
    key: { KEY_OBJECT },
    environment: 'mainnet',
});
```

This function call posts the signed transaction on Arweave's `mainnet`.

</details>

### Returned Data

The function call returns the following data depending on input parameters:

* A signed object of type [Transaction](https://docs.arweave.org/developers/server/http-api#field-definitions) is returned by Arweave.
* A status object is also returned. `status: 200` and `statusText: 'OK'` indicates a successful post request on Arweave.
  * The transaction is posted on the selected `environment` (`local` or `mainnet`).
