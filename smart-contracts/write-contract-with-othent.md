---
description: Write to a smart contract with Othent
---

# Write Contract with Othent

[Othent](https://docs.othent.io/developers/sdk) is library facilitating the onboarding of users from web2 to web3 through account abstraction. The authentication protocol offers a number of "wallet-less" functions for the same. Users can connect and interact with applications using web2 technologies like email accounts with the help of Othent.

The `writeContractWOthent` function enables interacting with a deployed contract based on the input parameters.

{% hint style="info" %}
The `writeContractWOthent` function currently supports only [internal write interactions](https://docs.warp.cc/docs/sdk/advanced/internal-calls#internal-writes) with contracts deployed using the [warp-sdk](https://academy.warp.cc/docs/sdk/overview).
{% endhint %}

{% hint style="info" %}
Ensure you have pop-ups enabled in your browser for the URL you'll be using this function in.
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { writeContractWOthent } from 'arweavekit/contract'

const writeResult = await writeContractWOthent({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `apiId: string` : Use of any Othent function requires an `apiId` which can be fetched from [othent.io](https://othent.io/). Towards the bottom of the linked page, the `Get your API ID` button provides the same.
* `othentFunction: string` : The `othentFunction` param informs the protocol's backend on the type of interaction to network. For the `writeContractWOthent` function, the required input is `'sendTransaction'`.
* `data: object` : The `data` field helps the function call understand details for interaction with a contract.
  * `toContractId: string` : The `id` of the contract to be interacted with.
  * `toContractFunction: string` : The function within the specified contract to be called. Every SmartWeave contract generally defines conditionals for multiple functions within it and depending on the function name passed in as input, the particular function logic is executed.
  * `txnData : object` : The data are the input parameters required by a function within the contract to run successfully.
*   `tags : array` (optional) : Tags can be added to any write interaction for ease of indexing and querying. Every tag must be passed in as an object in the tags array. The syntax for adding tags is as follows:

    ```javascript
    tags: [{ 'name': key_name, 'value': some_value},
            { 'name': key_name2, 'value': some_value2}]
    ```

{% hint style="info" %}
The `environment` does not need to be specified for `writeContractWOthent` as it only supports `mainnet` interactions, currently.
{% endhint %}

<details>

<summary>Example</summary>

```javascript
const writeResult = await writeContractWOthent({
  apiId: string,
  othentFunction: 'sendTransaction', 
  data: {
    toContractId: '2W9NoIJM1SuaFUaSOJsui_5lD_NvCHTjez5HKe2SjYU', 
    toContractFunction: 'createPost', 
    txnData: { blog_entry: 'Hello World!'} 
  }, 
  tags: [ {name: 'Test', value: 'Tag'} ]
});
```

This writes to the contract deployed by calling the function `createPost` from the contract logic and updating the state accordingly.

</details>

### Returned Data

The function call returns the following data:

* `success: boolean` : The `success` status of the write interaction.
* `transactionId: string` : The unique identifier for the write interaction. As every write interaction is a transaction, it has a corresponding `transactionId` associated with it for future reference.
