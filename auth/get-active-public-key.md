---
description: Get public key of active web wallet on Arweave
---

# Get Active Public Key

The `getActivePublicKey` function fetches the public key of the active web wallet.

{% hint style="info" %}
The ACCESS\_PUBLIC\_KEY permission must be granted either while calling `connect()` or `getPermissions()` in order to successfully use this function. Read more about permissions [here](https://github.com/arconnectio/ArConnect#permissions).&#x20;
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { ArConnect } from 'arweavekit/auth'

const response = await ArConnect.getActivePublicKey();
```

### Returned Data

The function call returns the following data:

```bash
[
    'ACTIVE_PUBLIC_KEY'
]
```

* `activePublicKey: array`: The key of the active web wallet.
