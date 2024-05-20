---
description: Get the details for a posted transaction
---

# Get Transaction

Get details about a transaction that has already been posted to the network with the help of the `getTransaction` function.

{% hint style="info" %}
This function is only valid for transactions for which the post request has already been sent to the network. Additionally, this function only works with transactions generated with the default param for network (i.e. the `arweave-js` library. Support for the Bundlr SDK is not available currently.
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { getTransaction } from 'arweavekit/transaction'

const data = await getTransaction({params});
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

```bash
{
    transaction: [TransactionObject]
}
```

* `transaction: Transaction` : An object of type [Transaction](https://docs.arweave.org/developers/server/http-api#field-definitions) is returned by Arweave.
