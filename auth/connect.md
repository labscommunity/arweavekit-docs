---
description: Connecting a web wallet on Arweave
---

# Connect

The `connect` function connects an application to a web wallet and gives the application appropriate permissions based on the input parameters.

### Basic Syntax

The function is called as follows:

```javascript
import { ArConnect } from 'arweavekit/auth'

const response = await ArConnect.connect({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `permissions: array` : The permissions array consists of specific permissions that the application requires to perform actions on behalf of the user. Currently there are 8 permissions available. Read more [here](https://github.com/arconnectio/ArConnect#permissions).
* `appInfo: object` (optional) : Additional information about application like `name` and `logo`. This is suitable for custom applications trying to make a connection.
* `gateway: object` (optional) : The gateway configuration to be used while connecting web wallet to application.
  * `host: string` : The Hostname or IP address for a Arweave Host.
  * `port: number` : The port for the gateway.
  * `protocol: 'http' | 'https'` : The network protocol for the gateway.

### Returned Data

The function call returns a `void`. However, the function can be coupled with conditionals to perform user authentication and display gated information.
