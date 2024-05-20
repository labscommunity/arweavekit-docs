---
description: Create a smart contract on Arweave
---

# Create Contract

The `createContract` function creates a contract based on the input parameters. The contract can be created either on the `mainnet` or on a `testnet/ local network` for testing purposes.

### Basic Syntax

The function is called as follows:

```javascript
import { createContract } from 'arweavekit/contract'

const contract = await createContract({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `wallet: ArWallet | string` (optional) : The wallet for deploying the contract with. The type `ArWallet` basically checks for Arweave wallet of the type `JWKInterface` and type `String` expects the private key of the Ethereum wallet and if the wallet param is not passed, it falls back to check for a web-based wallet like [Metamask](https://metamask.io/) or [ArConnect](https://www.arconnect.io/). When falling back to a web wallet, an Ethereum Wallet (like Metamask) is triggered since contract functions use bundling by default, which supports EVM web wallets. If this attempt fails, the function will retry with an Arweave Web Wallet (like ArConnect or arweave.app). The wallet key file can be loaded as follows and passed to the wallet param:

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
`Arweave JWK` or `Ethereum Private key` is needed as a wallet parameter in the node environment. And, the wallet param needed not to be passed in the browser environment for use with `Arconnect` or an `Ethereum-based wallet (like Metamask)`.
{% endhint %}

{% hint style="info" %}
&#x20;In order to explicitly use an Arweave Web Wallet, `use_wallet` must be passed into the wallet param, which also disables bundling in order to successfully process the function call.
{% endhint %}

{% hint style="info" %}
For deploying a contract on `mainnet` please ensure the wallet of choice has funds.
{% endhint %}

* `initialState: string` : The initial state of information for the contract at the time of deployment in `string` format. The `initState` file can be passed in directly as a string or read from a file as follows:

```javascript
import { readFileSync } from 'fs';

const initState = readFileSync('ABSOLUTE_FILE_PATH', 'utf-8');
```

*   `contractSource: string | Buffer` : The contract source parameter can either be the source code or a transaction ID to an existing source code. Contract data (logic) read from a file that must be encoded in `utf-8` a format that returns a `string`. The contract source file can be loaded or it can be a contract source transaction ID as follows:\


    <pre class="language-javascript"><code class="lang-javascript">// Load contract source code
    <strong>const contractSource = readFileSync('ABSOLUTE_FILE_PATH', 'utf-8');
    </strong>
    // Or, it can be a contract source transaction ID
    const contractSource = "Of9pi--Gj7hCTawhgxOwbuWnFI1h24TTgO5pw8ENJNQ"
    </code></pre>
*   &#x20;`tags: array` (optional) : Tags can be added to any transaction for ease of indexing and querying. The syntax for adding tags is as follows:\


    ```javascript
    tags: [
      { name: "key_name1", value: "some_value1" },
      { name: "key_name2", value: "some_value2" },
    ]
    ```

    The `name` is the key for a given `value` that can be used for querying the transaction in the future. By default, the library adds the `'ArweaveKit' : '1.5.1'` tag on the backend to help identify the library and version used to deploy the function.
*   `data: object` (optional): It accepts `Content-Type` of the data and the `body` of the data so the data can be accessed with the same deployed contract transaction ID making it an atomic asset.\


    ```typescript
    data: {
      'Content-Type': 'text/html',
      body: '<p>Hello World!</p>',
    }
    ```
* `evaluationManifest : object` (optional): The evaluation manifest defines rules that must be used when evaluating the contract being deployed. This includes evaluation options as well as any plugins that the contract deployment may need. Read more about [evaluation options](https://academy.warp.cc/docs/sdk/advanced/evaluation-options) and [contract manifests](https://academy.warp.cc/docs/sdk/advanced/manifest) to learn about the available configurations and their uses. Learn more about plugins [here](https://academy.warp.cc/docs/sdk/advanced/plugins/overview).
* `environment: 'local' | 'testnet' | 'mainnet'` : The environment of choice to create the smart contract in. The `testnet` is a pseudo-testing environment created on top of the `mainnet` with the help of custom tags.

{% hint style="info" %}
An `arlocal` instance must be running on the port <mark style="color:red;">`1984`</mark> for the function to work with the local environment. To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

* `strategy : 'arweave' | 'ethereum' | 'both'` (optional) : The strategy specifies the wallet (Ethereum or Arweave) to be used for contract creation. While the wallet can be determined by the wallet param passed in, it can be beneficial to pass in when using the browser environment. However, by default, the strategy is set to `'both'` and thus tries the function call with Ethereum first and fallback on an Arweave Wallet.

<details>

<summary>Example</summary>

<pre class="language-javascript"><code class="lang-javascript">const contract = await createContract({
    wallet: wallet_key,
    initialState: initState,
<strong>    contractSource: contractSource,
</strong>    environment: 'local',
});
</code></pre>

This uploads the contract logic on the local network along with the initial state with the help of the wallet provided.

</details>

### Returned Data

The function call returns the following data:

```bash
{
    status: {
        code: 200,
        message: 'SUCCESSFUL',
    },
    contract: object,
    contractTxId: 'CONTRACT_TRANSACTION_ID',
}
```

* `contract: ContractDeploy` : The contract object has relevant transaction IDs for future interactions. Read more about it [here](https://github.com/warp-contracts/warp/blob/ffd2c414a3b14ab8b2fe690eae50c1bd7603b51a/src/contract/deploy/CreateContract.ts#L53).
* `contractTxId: string` : The `contractTxId` is a unique identifier for further interactions with the contract like read and write operations. It is an instance of the contract source that is uploaded on the network.
* `status: object` : The `result` object returns easy to understand information showing the status of the contract deployment. `code: 200` and `message: 'SUCCESSFUL'` indicate that the contract has been successfully deployed to the network.
