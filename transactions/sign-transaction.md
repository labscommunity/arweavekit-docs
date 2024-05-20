---
description: Sign a created transaction
---

# Sign Transaction

As seen earlier, the transaction process has been split in 3 steps. Once a transaction has been created, it must be signed. The signature is a unique identifier created by hashing the input parameters provided while creating the transaction and wallet information of the signer. This is useful for verification purposes and prevention of forgery.

The `signTransaction` function creates a signature for a transaction.

### Basic Syntax

The function is called as follows:

```javascript
import { signTransaction } from 'arweavekit/transaction'

const signedTransaction = await signTransaction({params}) 
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `key: JWKInterface` (optional): The private key for the wallet signing the transaction. When using in web apps, this field can be left empty or the `use_wallet` string can be passed in to trigger a web wallet. The wallet key file can be loaded as follows:

```javascript
import { readFileSync } from 'fs';

const key = JSON.parse(readFileSync('wallet.json').toString());
```

* `environment: 'local' | 'mainnet'` (optional) : The environment on which the transaction was created.

{% hint style="info" %}
An `arlocal` instance must be running on port <mark style="color:red;">`1984`</mark> for the function to work with the local environment. To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

* `createdTransaction: object` : The transaction object created in the earlier step.
* `postTransaction: boolean` (optional): This boolean enables the posting of the transaction to Arweave using the `signTransaction` function itself.

<details>

<summary>Example</summary>

```javascript
const signedTransaction = await signTransaction({
    createdTransaction: createdTransaction,
    key: { KEY_OBJECT },
    environment: 'mainnet',
});
```

This call signs a created transaction on `mainnet` on a node environment.

</details>

### Returned Data

The function call returns the following data depending on input parameters:

* A signed object of type [Transaction](https://docs.arweave.org/developers/server/http-api#field-definitions) is returned by Arweave.
  * The `signature` key will be populated with a base64URL encoded signature hash with the help of the RSA algorithm.
  * The `id` of a transaction is only received after posting the transaction on Arweave.
  * On selecting the `postTransaction` option the function returns a status object along with the transaction object. `status: 200` and `statusText: 'OK'` indicates a successful post request on Arweave.
  * The transaction is signed on the selected `environment` (`local` or `mainnet`).
