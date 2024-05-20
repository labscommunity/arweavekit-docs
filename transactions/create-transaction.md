---
description: Create a transaction on Arweave
---

# Create Transaction

The `createTransaction` function creates a transaction based on the input parameters. The transaction can either be a data upload transaction or a wallet to wallet (token transfer) transaction.

### Basic Syntax

The function is called as follows:

<pre class="language-javascript"><code class="lang-javascript"><strong>import { createTransaction } from 'arweavekit/transaction'
</strong>
const transaction = await createTransaction({params});
</code></pre>

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `type: 'data' | 'wallet'` : The type of transaction to be created. A `data` type transaction uploads data on Arweave whereas a `wallet` type transaction transfers tokens from one wallet to another.
* `key: JWKInterface` (optional) : The private key for the wallet address to be fetched. The wallet key is optional for default transaction creation as no key is needed until signing a transaction, however, it must be passed in if the `useBundlr` or `signAndPost` option is set to `true`. The wallet key file can be loaded as follows:

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

* `environment: 'local' | 'mainnet'` : The environment for creating transactions. As this is only one part of the three step process of uploading transactions to Arweave, it is important that the transaction is signed and posted in the same environment it is created on.

{% hint style="info" %}
An `arlocal` instance must be running on port <mark style="color:red;">`1984`</mark> for the function to work with the local environment. To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

{% hint style="warning" %}
Currently, the Bundlr SDK only supports the `mainnet` environment.
{% endhint %}

* `target: string` (optional) : The wallet address to which the wallet to wallet transaction must be sent.

{% hint style="info" %}
The `target` must be accompanied with a `quantity` , else it sends a transaction with `0` tokens by default.
{% endhint %}

* `quantity: string` (optional) : The quantity specifies the units of **Winston** to be sent in a wallet to wallet transaction.

{% hint style="info" %}
The `quantity` must be accompanied with a `target` wallet address.
{% endhint %}

{% hint style="info" %}
**Winston** is the smallest possible unit of **AR**, similar to a [satoshi](https://en.bitcoin.it/wiki/Satoshi\_\(unit\)) in Bitcoin, or [wei](http://ethdocs.org/en/latest/ether.html#denominations) in Ethereum.

**1 AR** = 1000000000000 Winston (12 zeros) and **1 Winston** = 0.000000000001 AR.
{% endhint %}

* `data: string | Uint8Array | ArrayBuffer` (optional) : To create a data type transaction, this optional parameter can be passed in. The data can be passed as a `string`, `Uint8Array` or an `ArrayBuffer` (as preferred by the network).
* `options` : Additional options can be passed in as a JSON object.&#x20;
  *   &#x20;`tags: array` (optional) : Tags can be added to any transaction for ease of indexing and querying. The syntax for adding tags is as follows:

      ```javascript
      tags: [{ 'name': key_name, 'value': some_value},
              { 'name': key_name2, 'value': some_value2}]
      ```

      The `name` is the key for a given `value` that can be used for querying the   transaction in the future. By default the library adds the `'ArweaveKit' : '1.5.1'` tag on the backend to help identify the library and version used to deploy the function.
  * `signAndPost: boolean` (optional) : By default, the transaction process on Arweave has three steps to reduce the computation time, and provide convenience and customisation. However, by setting this option to `true`, the function signs and posts the transaction on chain in the same function call.
  * `useBundlr: boolean` (optional) : Creates the transaction using [bundlr network](https://docs.bundlr.network/docs/client/transactions). Only `data` type transactions can use this option. If the data size is under 100kB the transaction does not require any fees for processing through Bundlr.

{% hint style="warning" %}
Currently, the Bundlr SDK only supports data based transactions and only on the `mainnet`.
{% endhint %}

{% hint style="warning" %}
The `option` to `signAndPost` must be set to `true` for using `Bundlr`. Transactions using Bundlr will be signed and posted to the network by default as there is no support for signing and uploading Bundlr transactions in separate steps.
{% endhint %}

{% hint style="warning" %}
Web Transactions using Bundlr will fallback on Arweave in case of failure.
{% endhint %}

<details>

<summary>Example</summary>

<pre class="language-javascript"><code class="lang-javascript"><strong>const transaction = await createTransaction({
</strong><strong>    key: { KEY_OBJECT },
</strong><strong>    type: 'wallet',
</strong>    quantity: '1000000',
    target: 'TARGET_WALLET_ADDRESS',
    environment: 'mainnet',
    options: {
        tags: [{ 'name': 'key_name', 'value': 'some_value'}],
    },
});
</code></pre>

This call creates `wallet` type transaction on the `mainnet`  and adds the tags that we have defined. This needs to be signed and posted in the consequent steps to successfully upload on Arweave.

</details>

### Returned Data

The function call returns the following data depending on input parameters:

* Default transaction (when `useBundlr` is `false`):
  * An object of type [Transaction](https://docs.arweave.org/developers/server/http-api#field-definitions) is returned by Arweave.
  * The data related key value pairs hold information when `data` prop is passed in.
  * The target and quantity fields have in formation for wallet-to-wallet transactions.
  * The `signature` key has no information until the transaction is signed.
  * The `id` of a transaction is only received after calling the `postTransaction` function (basically, when the transaction is posted on Arweave).
  * On selecting the `signAndPost` option the function returns a status object along with the transaction object. `status: 200` and `statusText: 'OK'` indicates a successful post request on Arweave.
  * The transaction is created on the selected `environment` (`local` or `mainnet`).
* When the `useBundlr` option is set to `true:`
  * An object of type [Bundlr Transaction](https://github.com/Bundlr-Network/js-sdk/blob/12d5e57df8d82ca277106ca08e4787909ee3eede/src/common/transaction.ts#L11) and an object containing the `id` of the posted transaction and the `timestamp` are returned.
  * The `Bundlr Transaction` object consists information regarding the network, currency, data to be posted, tags, etc.
  * The `environment` is always `mainnet`.
* A few errors help identify the correct parameters in case any might be missing or not as expected.&#x20;
