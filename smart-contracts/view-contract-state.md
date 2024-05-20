---
description: View from a smart contract on Arweave
---

# View Contract State

The `viewContractState` function enables calling a contract's read function and getting the result based on the input parameters.

{% hint style="info" %}
To retrieve the state from a contract, it is recommended to utilize the [readContractState](read-contract-state.md) function.
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { viewContractState } from 'arweavekit/contract'

const viewResult = await viewContractState({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `wallet: ArWallet | string` (optional) : The wallet for viewing the contract with. The type `ArWallet` basically checks for Arweave wallet of the type `JWKInterface` and type `String` expects the private key of the Ethereum wallet and if the wallet param is not passed, it falls back to check for a web-based wallet like [Metamask](https://metamask.io/) or [ArConnect](https://www.arconnect.io/). When falling back to a web wallet, an Ethereum Wallet (like Metamask) is triggered since contract functions use bundling by default, which supports EVM web wallets. If this attempt fails, the function will retry with an Arweave Web Wallet (like ArConnect or arweave.app). The wallet key file can be loaded as follows and passed to the wallet param:

```javascript
import { readFileSync } from 'fs';

// Arweave JWK
const key = JSON.parse(readFileSync('wallet.json').toString());

// Ethereum Private Key
const key = readFileSync('privatekey.txt').toString();

// Now pass key to wallet param as wallet: key
```

{% hint style="info" %}
Wallet param is useful if the read functions of the contract uses the caller input. `Arweave JWK or Ethereum Private key` is needed as a wallet parameter in the node environment. And, the wallet param needed not to be passed in the browser environment for use with `Arconnect or an Ethereum-based wallet (like Metamask)`.
{% endhint %}

* `environment: 'local' | 'testnet' | 'mainnet'` : The environment in which the smart contract was created in. The `testnet` is a pseudo-testing environment created on top of the `mainnet` with the help of custom tags.

{% hint style="info" %}
If the contract was created in a `local` environment, please make sure that `arlocal` is running in the background to be able to interact with the contract. To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

* `evaluationOptions : object` (optional) : Evaluation options define rules on how a contract will be evaluated during view state interactions. Read more about [evaluation options](https://academy.warp.cc/docs/sdk/advanced/evaluation-options) to learn about the available configurations and their uses.
* `contractTxId: string` : The `contractTxId` is a unique identifier received upon contract creation. This helps `viewContractState` identify the contract to interact with.
* `cacheOptions : object` (optional) : Contract state is cached for fast retrieval and seamless experience. Custom configurations can be passed in as an object for more control over the caching process. This includes an `inMemory` option enabling the storage of cache in local memory. By default, the contract state is cached in a database. The `dbLocation` can be configured with the options outlined in these [docs](https://academy.warp.cc/docs/sdk/advanced/cache).
* `strategy : 'arweave' | 'ethereum' | 'both'` (optional) : The strategy specifies the wallet (Ethereum or Arweave) to be used for contract view state interaction. While the wallet can be determined by the wallet param passed in, it can be beneficial to pass in when using browser environments. However, by default, the strategy is set to `'both'` and thus tries the function call with Ethereum first and fallback on an Arweave Wallet.
* `options: Object` : The input arguments for the appropriate view state call with the contract. For the following sample contract:

```javascript
export function handle(state, action) {
  if (action.input.function === 'initialize') {
    state.counter = 10
  } else if (action.input.function === 'fifty') {
    state.counter = 50
  } else if (action.input.function === 'counter') {
    return { result: state.counter }
  }
  return { state }
}
```

An example for options would be: `options: { function: 'counter' }.`

* `connectWallet: boolean` (optional): It decides whether to view the state by connecting to the wallet or without connecting to the wallet. By default, its value is `true`.

<details>

<summary>Example</summary>

```javascript
const viewResult = await viewContractState({
  environment: 'testnet',
  contractTxId: 'CONTRACT_TRANSACTION_ID',
  wallet: wallet_key,
  options: { function: 'counter' },
});

/**
// example output viewResult
{
  viewContract: {
    type: 'ok',
    result: 10,
    state: {
      counter: 10
    }
  },
  result: { status: 200, statusText: 'SUCCESSFUL' }
}
*/
```

This calls the contract with options i.e. function `counter` and get the result.

</details>

### Returned Data

The function call returns the following data:

```json
{
  viewContract: {
    type: InteractionResultType,
    result: Result,
    state: State,
  },
  result: { status: 200, statusText: 'SUCCESSFUL' }
}
```

* `viewContract: InteractionResult<State, Result>`: The `viewContract` object has metadata relevant to the view state operation. Read more about it [here](https://github.com/warp-contracts/warp/blob/276b43d04bbd6e186fbf71dac297f72c13c633a8/src/core/modules/impl/HandlerExecutorFactory.ts#L284).
  * `type: InteractionResultType`: Result of the view state interaction. It can have a value of 'ok' , 'error' or 'exception'.
  * `state: State`: The `state` object is the latest version of information (variables and interactions with them) that is stored on the chain and associated with the contract. The `viewContractState` assumes that the view interaction has been processed as expected and returns the updated state from the cache.
  * `result: Result`: It is the value returned from the contract's read function as result.
* `result: object` : The `result` object returns easy to understand information showing the status of the view state. `status: 200` and `statusText: 'SUCCESSFUL'` indicate that view state interaction with the options is successful.
