---
description: Get wallet names of web wallets on Arweave
---

# Get Wallet Names

The `getWalletNames` function fetches the wallet names of the web wallets in the browser extension.

{% hint style="info" %}
The ACCESS\_ALL\_ADDRESSES permission must be granted either while calling `connect()` or `getPermissions()` in order to successfully use this function. Read more about permissions [here](https://github.com/arconnectio/ArConnect#permissions).&#x20;
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { ArConnect } from 'arweavekit/auth'

const response = await ArConnect.getWalletNames();
```

### Returned Data

The function call returns the following data:

```bash
{
    'WALLET_ADDRESS_1': 'WALLET_NAME_1',
    'WALLET_ADDRESS_2': 'WALLET_NAME_2'
}
```

* `walletNames: object`: An object consisting of key-value pairs of the wallet addresses and associated wallet names.
