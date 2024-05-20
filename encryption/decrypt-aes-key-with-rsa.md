---
description: Decrypt an AES Key with an RSA Private Key
---

# Decrypt AES Key with RSA

The `decryptAESKeyWithRSA` performs asymmetric decryption using an `RSA Private Key` and the `RSA-OAEP` algorithm. The permissions are requested with the help of the `Arweave Wallet (Window Object)` in a browser environment if no wallet or `use_wallet` is passed. The node environment expects Arweave JWK to be passed.

{% hint style="info" %}
Installation of [`ArConnect`](https://www.arconnect.io/) is suggested for successful use of this function in a browser environment.
{% endhint %}

### Basic Syntax

The function is called as follows:

```javascript
import { decryptAESKeyWithRSA } from 'arweavekit/encryption';

const decryptedAESKey = await decryptAESKeyWithRSA({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `key: Uint8Array` : Th`e encrypted AES key received from the encryptAESKeyWithRSA function.`
* `wallet: ArWallet`(optional): A value of type `JWKInterface` or `use_wallet` can be passed. If `use_wallet` or nothing is passed to this param, it expects `ArConnect` to be installed to run the decryption successfully.

<details>

<summary>Example</summary>

```javascript
// In a browser environment, use_wallet or nothing can be passed.
const wallet = "use_wallet"
// In a node environment, Arweave wallet JWK can be passed.
const wallet = JSON.parse(fs.readFileSync('wallet.json').toString());

const decryptedAESKey = await decryptAESKeyWithRSA({
    key: Uint8Array,
});
```

This decrypts the provided `AES Key` using the `RSA-OAEP` algorithm.

</details>

### Returned Data

The function call returns the following data:

```bash
{
    decryptedKey: string,
}
```

* `decryptedKey: string` : The `AES` key decrypted using an `RSA Public Key` returned as a `Base64 string`.
