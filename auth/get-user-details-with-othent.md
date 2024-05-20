---
description: Getting details of user logged in using Othent
---

# Get User Details with Othent

The `userDetails` function returns details of the logged in user associated with their user account.

{% hint style="info" %}
Ensure you have pop-ups enabled in your browser for the URL you'll be using this function in.
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { Othent } from 'arweavekit/auth'

const result = await Othent.userDetails({params});
```

### Input Parameters

* `apiId: string` : Use of any Othent function requires an `apiId` which can be fetched from [othent.io](https://othent.io/). Towards the bottom of the linked page, the `Get your API ID` button provides the same.

<details>

<summary>Example</summary>

```javascript
const result = await Othent.userDetails({
    apiId: string
});
```

This function get the details of the connected user associated with their connected account.

</details>

### Returned Data

The function call returns the following data:

```bash
{
    contract_id: string,
    given_name: string,
    family_name: string,
    nickname: string,
    name: string,
    picture: string,
    locale: string,
    email: string,
    email_verified: string,
    sub: string,
    success?: string,
    message?: string
}
```

* `contract_id: string` : The `contract_id` is the wallet address associated with a user's email account, provided to the user at the time of registration with Othent.
* `given_name: string` : The `given_name` is the connected user's first name associated with the email account.
* `family_name: string` : The `family_name` is the connected user's last name associated with the email account.
* `nickname: string` : The `nickname` is the connected user's initials associated with the email account.
* `name: string` : The `name` is the connected user's given\_name and family\_name joined together.
* `picture: string` : The `picture` is the connected user's profile picture associated with the email account.
* `locale: string` : The `locale` is the connected user's preferred language associated with the email account.
* `email: string` : The `email` is the connected user's email address.
* `email_verified: string` : The `email_verified` holds information the confirmation status of the email.
* `sub: string` : The `sub` is a unique id for Othent's reference.
* `success: string` (optional) : The `success` status of function call.
* `message: string` (optional) : Any `message` to be returned with function call.
