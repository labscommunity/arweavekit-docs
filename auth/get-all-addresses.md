---
description: Get addresses of web wallets on Arweave
---

# Get All Addresses

The `getAllAddresses` function fetches the wallet addresses of the web wallets in the browser extension.

{% hint style="info" %}
The ACCESS\_ALL\_ADDRESSES permission must be granted either while calling `connect()` or `getPermissions()` in order to successfully use this function. Read more about permissions [here](https://github.com/arconnectio/ArConnect#permissions).&#x20;
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { ArConnect } from 'arweavekit/auth'

const response = await ArConnect.getAllAddresses();
```

### Returned Data

The function call returns the following data:

```bash
[
    'WALLET_ADDRESS_1',
    'WALLET_ADDRESS_2'
]
```

* `walletAddresses: array`: A list of all the added wallet addresses.
