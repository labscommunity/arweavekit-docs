---
description: Getting address of active web wallet on Arweave
---

# Get Active Address

The `getActiveAddress` function fetches the address of the active web wallet.

{% hint style="info" %}
The `ACCESS_ADDRESS` permission must be granted either while calling `connect()` or `getPermissions()` in order to successfully use this function. Read more about permissions [here](https://github.com/arconnectio/ArConnect#permissions).&#x20;
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { ArConnect } from 'arweavekit/auth'

const address = await ArConnect.getActiveAddress();
```

### Returned Data

The function call returns the following data:

```bash
'WALLET_ADDRESS'
```

* `address: string` : The wallet address of the active web wallet.
