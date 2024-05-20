---
description: Write to a smart contract on Arweave
---

# Write Contract

The `writeContract` function enables interaction with a deployed contract based on the input parameters.

### Basic Syntax

The function is called as follows:

<pre class="language-javascript"><code class="lang-javascript">import { writeContract } from 'arweavekit/contract'

<strong>const writeResult = await writeContract({params});
</strong></code></pre>

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `environment: 'local' | 'testnet' | 'mainnet'` : The environment in which the smart contract was created in. The `testnet` is a pseudo-testing environment created on top of the `mainnet` with the help of custom tags.

{% hint style="info" %}
If the contract was created in a `local` environment, please make sure that`arlocal` is running in the background to be able to interact with the contract. To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

* `contractTxId: string` : The `contractTxId` is a unique identifier received upon contract creation. This helps the `writeContract` to identify the contract to interact with.
* `wallet: ArWallet | string` (optional) : The wallet for writing the contract with. The type `ArWallet` basically checks for Arweave wallet of the type `JWKInterface` and type `String` expects the private key of the Ethereum wallet and if the wallet param is not passed, it falls back to check for a web-based wallet like [Metamask](https://metamask.io/) or [ArConnect](https://www.arconnect.io/). When falling back to a web wallet, an Ethereum Wallet (like Metamask) is triggered since contract functions use bundling by default, which supports EVM web wallets. If this attempt fails, the function will retry with an Arweave Web Wallet (like ArConnect or arweave.app). The wallet key file can be loaded as follows and passed to the wallet param:

```javascript
import { readFileSync } from 'fs';

// Arweave JWK
const key = JSON.parse(readFileSync('wallet.json').toString());

// Ethereum Private Key
const key = readFileSync('privatekey.txt').toString();

// Now pass key to wallet param as wallet: key
```

```javascript
// For passing to wallet param using the arweave.app wallet
import { ArweaveWebWallet } from "arweave-wallet-connector";

const webWallet = new ArweaveWebWallet();
webWallet.setUrl("arweave.app");
await webWallet.connect();

// Now pass webWallet to wallet param as wallet: webWallet
```

{% hint style="info" %}
`Arweave JWK` or `Ethereum Private key` is needed as a wallet parameter in the node environment. And, the wallet param needed not to be passed in the browser environment for use with Arconnect or an Ethereum-based wallet (like Metamask).
{% endhint %}

* `options: Object` : The input arguments for the appropriate write interaction call with the contract. For the following sample contract:

<pre class="language-javascript"><code class="lang-javascript">export function handle(state, action) {
  if (action.input.function === 'initialize') {
    state.counter = 10
  }
  if (action.input.function === 'fifty') {
    state.counter = 50
  }
  return { state }
<strong>}
</strong></code></pre>

&#x20;      The options would be: `options: { function: 'initialize' }`.

*   `tags: array` (optional) : Tags can be added to any transaction for ease of indexing and querying. The syntax for adding tags is as follows:

    ```javascript
    tags: [
      { name: "key_name1", value: "some_value1" },
      { name: "key_name2", value: "some_value2" },
    ]
    ```

    The `name` is the key for a given `value` that can be used for querying the transaction in the future. By default, the library adds the `'ArweaveKit' : '1.5.1'` tag on the backend to help identify the library and version used to deploy the function.
* `vrf : boolean` (optional) : VRF enables the use of verifiable randomness in contracts wherever random values are required. Read more about VRF [here](https://academy.warp.cc/docs/sdk/advanced/vrf).
* `evaluationOptions : object` (optional) : Evaluation options define rules on how a contract will be evaluated during write interactions. Read more about [evaluation options](https://academy.warp.cc/docs/sdk/advanced/evaluation-options) to learn about the available configurations and their uses.
* `strategy : 'arweave' | 'ethereum' | 'both'` (optional) : The strategy specifies the wallet (Ethereum or Arweave) to be used for contract writing. While the wallet can be determined by the wallet param passed in, it can be beneficial to pass in when using browser environments. However, by default, the strategy is set to `'both'` and thus tries the function call with Ethereum first and fallback on an Arweave Wallet.
* `cacheOptions : object` (optional) : Contract state is cached for fast retrieval and seamless experience. Custom configurations can be passed in as an object for more control over the caching process. This includes an `inMemory` option enabling the storage of cache in local memory. By default, the contract state is cached in a database. The `dbLocation` can be configured with the options outlined in these [docs](https://academy.warp.cc/docs/sdk/advanced/cache).

<details>

<summary>Example</summary>

```javascript
const writeResult = await writeContract({
  environment: 'testnet',
  contractTxId: 'CONTRACT_TRANSACTION_ID',
  wallet: wallet_key,
  options: { function: 'initialize' },
});
```

This writes to the contract deployed by calling the function `initialize` from the contract logic and updating the state accordingly.

</details>

### Returned Data

The function call returns the following data:

```bash
writeContract: {
    bundlrResponse: [BundlrResponse]
    },
    originalTxId: 'ORIGINAL_TRANSACTION_ID'
},
state: [Object],
result: { status: 200, statusText: 'SUCCESSFUL' }
```

* `writeContract: WriteInteractionRespone` : The `writeContract` object has metadata relevant to the write operation.  Read more about it [here](https://github.com/warp-contracts/warp/blob/271ad999768abe14bb6a24e1149e3b770c0b405f/src/contract/Contract.ts#L19).
  * `bundlrResponse: BundlrResponse` : By default, the function uses [bundlr network](https://bundlr.network/) to perform the write operation and thus returns information related to the bundling of this write operation.
  * `originalTxId: string` : The `originalTxId` is the unique identifier that can be used to find information about this write operation on Arweave.
* `state: object` : The `state` object is the latest version of information (variables and interactions with them) that is stored on the chain and associated with the contract. The `writeContract` assumes that the write interaction has been processed as expected and returns the updated state from the cache.
* `result: object` : The `result` object returns easy to understand information showing the status of the write interaction. `status: 200` and `statusText: 'SUCCESSFUL'` indicate that information has been successfully written to the contract.
