---
description: Getting permissions from web wallet on Arweave
---

# Get Permissions

The `getPermissions` function requests the active web wallet for permissions on behalf of the application.

### Basic Syntax

The function is called as follows:

```javascript
import { ArConnect } from 'arweavekit/auth'

const response = await ArConnect.getPermissions();
```

### Returned Data

The function call returns the following data:

```bash
[
    'PERMISSION_1',
    'PERMISSION_2'
]
```

* `permissions: array`: A list of all the permissions provided to the application. Read more about the available permissions [here](https://github.com/arconnectio/ArConnect#permissions).
