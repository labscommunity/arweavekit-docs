---
description: Post a transaction on Arweave with Othent
---

# Create and Post Transaction with Othent

[Othent](https://docs.othent.io/developers/sdk) is library facilitating the onboarding of users from web2 to web3 through account abstraction. The authentication protocol offers a number of "wallet-less" functions for the same. Users can connect and interact with applications using web2 technologies like email accounts with the help of Othent.

The `createAndPostTransactionWOthent` function enables interacting with a deployed contract based on the input parameters.

### Basic Syntax

{% hint style="info" %}
Ensure you have pop-ups enabled in your browser for the URL you'll be using this function in.
{% endhint %}

The function is called as follows:

```javascript
import { createAndPostTransactionWOthent } from 'arweavekit/transaction'

const transaction = await createAndPostTransactionWOthent({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `apiId: string` : Use of any Othent function requires an `apiId` which can be fetched from [othent.io](https://othent.io/). Towards the bottom of the linked page, the `Get your API ID` button provides the same.
* `othentFunction: string` : The `othentFunction` param informs the protocol's backend on the type of interaction to network. For the `createAndPostTransactionWOthent` function, the required input is `'uploadData'`.
* `data: object` : The `data` field is the data to be uploaded on the network. Currently, the function supports data uploads of type `File`. This can be a file of any format.
*   `tags : array` (optional) : Tags can be added to any data for ease of indexing and querying. Every tag must be passed in as an object in the tags array. The syntax for adding tags is as follows:

    ```javascript
    tags: [{ 'name': key_name, 'value': some_value},
            { 'name': key_name2, 'value': some_value2}]
    ```
* `useBundlr: boolean` (optional) : Creates and posts the transaction using [bundlr network](https://docs.bundlr.network/docs/client/transactions). Only data type transactions can use this option. If the data size is under 100kB the transaction does not require any fees for processing through Bundlr.

{% hint style="info" %}
The `environment` does not need to be specified for `createAndPostTransactionWOthent` as it only supports `mainnet` interactions, currently.
{% endhint %}

<details>

<summary>Example</summary>

```javascript
const postedTransaction = await createAndPostTransactionWOthent({
  apiId: string,
  othentFunction: 'uploadData', 
  data: image.png, 
  tags: [ {name: 'Test', value: 'Tag'} ]
});
```

This function uploads the input data (image) to the network along with the tags, after verifying the `apiId`.

</details>

### Returned Data

The function call returns the following data:

* `success: boolean` : The `success` status of the data upload request.
* `transactionId: string` : The unique identifier for the upload request. As every upload request is a transaction, it has a corresponding `transactionId` associated with it for future reference.
