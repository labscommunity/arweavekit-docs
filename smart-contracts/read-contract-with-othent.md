---
description: Read from a smart contract with Othent
---

# Read Contract with Othent

[Othent](https://docs.othent.io/developers/sdk) is library facilitating the onboarding of users from web2 to web3 through account abstraction. The authentication protocol offers a number of "wallet-less" functions for the same. Users can connect and interact with applications using web2 technologies like email accounts with the help of Othent.

The `readContractWOthent` function enables interacting with a deployed contract based on the input parameters.

{% hint style="info" %}
Ensure you have pop-ups enabled in your browser for the URL you'll be using this function in.
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { readContractWOthent } from 'arweavekit/contract'

const readResult = await readContractWOthent({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `apiId: string` : Use of any Othent function requires an `apiId` which can be fetched from [othent.io](https://othent.io/). Towards the bottom of the linked page, the `Get your API ID` button provides the same.
* `contractTxId: string` : The `contractTxId` points to the contract that is requested to be read.

<details>

<summary>Example</summary>

```javascript
const readResult = await readContractWOthent({
  apiId: string,
  contractTxId: '2W9NoIJM1SuaFUaSOJsui_5lD_NvCHTjez5HKe2SjYU'
});
```

This reads the current state of the contract whose `id` is specified as input.

</details>

### Returned Data

The function call returns the following data:

* `state: object` : The `state` is the information/ data stored with a contract. The read call returns the latest version of the state for the specified contract as reflected on the network.
* `errors: object` : The `errors` object consists of metadata for any errors that may have occurred returning the read result or previous unsuccessful interactions with the contract.
* `validity : object` The `validity` is the validity of the returned state of a contract.
