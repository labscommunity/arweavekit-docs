---
description: Log out of Arweave applications using Othent
---

# Log Out with Othent

The `logOut` function lets users log out of applications built on Arweave using web2 technologies like email addresses.

{% hint style="info" %}
Ensure you have pop-ups enabled in your browser for the URL you'll be using this function in.
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { Othent } from 'arweavekit/auth'

const result = await Othent.logOut({params});
```

### Input Parameters

* `apiId: string` : Use of any Othent function requires an `apiId` which can be fetched from [othent.io](https://othent.io/). Towards the bottom of the linked page, the `Get your API ID` button provides the same.

<details>

<summary>Example</summary>

```javascript
const result = await Othent.logOut({
    apiId: string
});
```

This function logs out users from the connected application.

</details>

### Returned Data

The function call returns the following data:

```bash
{
    response: string
}
```

* `response: string` : The `response` returned on function call.
