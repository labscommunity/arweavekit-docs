---
description: Read from a smart contract on Arweave
---

# Read Contract State

The `readContractState` function enables reading the contract state from a deployed contract based on the input parameters.

{% hint style="info" %}
To retrieve the result from a contract's read function, it is recommended to utilize the [viewContractState](view-contract-state.md) function.
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { readContractState } from 'arweavekit/contract'

const readResult = await readContractState({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `environment: 'local' | 'testnet' | 'mainnet'` : The environment in which the smart contract was created in. The `testnet` is a pseudo testing environment created on top of the `mainnet` with the help of custom tags.

{% hint style="info" %}
If the contract was created in a `local` environment, please make sure that`arlocal` is running in the background to be able to interact with the contract. To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

* `evaluationOptions : object` (optional) : Evaluation options define rules on how a contract will be evaluated during reading contract state. Read more about [evaluation options](https://academy.warp.cc/docs/sdk/advanced/evaluation-options) to learn about the available configurations and their uses.
* `contractTxId: string` : The `contractTxId` is a unique identifier received upon contract creation. This helps the `writeContract` to identify the contract to interact with.
* `cacheOptions : object` (optional) : Contract state is cached for fast retrieval and seamless experience. Custom configurations can be passed in as an object for more control over the caching process. This includes an `inMemory` option enabling the storage of cache in local memory. By default, the contract state is cached in a database. The `dbLocation` can be configured with the options outlined in these [docs](https://academy.warp.cc/docs/sdk/advanced/cache).

<details>

<summary>Example</summary>

```javascript
const readResult = await readContractState({
      environment: 'testnet',
      contractTxId: 'CONTRACT_TRANSACTION_ID',
});
```

</details>

### Returned Data

The function call returns the following data:

```bash
readContract: SortKeyCacheResult {
    sortKey: '000000000000,0000000000000,0000000000000000000000000000000000000000000000000000000000000000',
    cachedValue: EvalStateResult {
      state: [Object],
      validity: {},
      errorMessages: {}
    }
},
result: { status: 200, statusText: 'SUCCESSFUL' }
```

* `readContract: SortKeyCacheResult` : The `readContract` object returns the `sortKey` and `cachedValue`. Read more [here](https://github.com/warp-contracts/warp/blob/e944cd7c0f0af7ed29de8593f4e5f9689e589525/src/cache/SortKeyCache.ts#L87).
  * `sortKey: string` : The `sortKey` is a value that [warp](https://warp.cc/) uses to sort contract transactions.
  * `cachedValue: EvalStateResult` : The `cachedValue` is an object that stores the state, the validity of the state and any errors faced while reading the state. If the `readContract` function is called immediately after a `writeContract` call, the cached state is optimistically updated assuming the write call occurs successfully, while the interaction continues to be processed on the actual network (in cases of using the `testnet` and `mainnet`.
* `result: object` : The `result` object returns easy to understand information showing the status of the read call. `status: 200` and `statusText: 'SUCCESSFUL'` indicate that information has been successfully read from the contract.
