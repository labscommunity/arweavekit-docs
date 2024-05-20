---
description: Get the transaction status of a posted transaction
---

# Get Transaction Status

There is a wait time involved between requesting to post a transaction on chain and it actually being posted.

The `getTransactionStatus` functions provides the status for a given transaction on whether it has been successfully posted on chain or is amidst processing.

{% hint style="info" %}
This function is only valid for transactions for which the post request has already been sent to the network. Additionally, this function only works with transactions generated with the default param for network (i.e. the `arweave-js` library. Support for the Bundlr SDK is not available currently.
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { getTransactionStatus } from 'arweavekit/transaction'

const status = await getTransactionStatus({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `transactionId: string` : The unique identification Id associated with a transaction.
* `environment: 'local' | 'mainnet'` : The environment on which the transaction was posted.

{% hint style="info" %}
An `arlocal` instance must be running on port <mark style="color:red;">`1984`</mark> for the function to work with the local environment. To create one, simply run `npx arlocal` in the command line. Learn more about `arlocal` [here](https://cookbook.arweave.dev/guides/testing/arlocal.html).
{% endhint %}

### Returned Data

The function call returns the following data:

```javascript
{
  status: 200,
  confirmed: {
    block_height: 1107205,
    block_indep_hash: 'O0VduHn7GsBx0jsLVKXSPpx_ue-GRXpX56_1hfmIOrVI9sQFVe1ABb8iDDLJBzlu',
    number_of_confirmations: 18358
  }
}
```

* `status: number` : The `status` is an indicator on whether the transaction has been successfully processed. It must return the value `200` for the same.
* `confirmed: object` :  The `confirmed` object contains additional information regarding the successful processing of the transaction.
  * `block_height: number` : The height or block number in which the transaction has been processed.
  * `block_indep_hash: string` : &#x20;
  * `number_of_confirmations: number` :  The number of blocks in the network that have been mined since processing of the given transaction.
