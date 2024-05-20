---
description: Encrypt an AES Key with an RSA Public Key
---

# Encrypt AES Key with RSA

The `encryptAESKeyWithRSA` performs asymmetric encryption using an `RSA Public Key` and the `RSA-OAEP` algorithm. The permissions are requested with the help of the `Arweave Wallet (Window Object)` in a browser environment if no wallet or `use_wallet` is passed. The node environment expects Arweave JWK to be passed.

{% hint style="info" %}
Installation of [`ArConnect`](https://www.arconnect.io/) is suggested for successful use of this function in a browser environment.
{% endhint %}

Asymmetric encryption is optimal for the encryption of strings (such as the `AES` key received in the previous function).

### Basic Syntax

The function is called as follows:

```javascript
import { encryptAESKeyWithRSA } from 'arweavekit/encryption';

const encryptedAESKey = await encryptAESKeyWithRSA({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `key: string` : The `AES` key used to encrypt data using the `encryptDataWithAES` function.
* `wallet: ArWallet`(optional): A value of type `JWKInterface` or `use_wallet` can be passed. If `use_wallet` or nothing is passed to this param, it expects `ArConnect` to be installed to run the encryption successfully.

<details>

<summary>Example</summary>

<pre class="language-javascript"><code class="lang-javascript"><strong>// In a browser environment, use_wallet or nothing can be passed.
</strong><strong>const wallet = "use_wallet"
</strong>// In a node environment, Arweave wallet JWK can be used.
const wallet = JSON.parse(fs.readFileSync('wallet.json').toString());

const encryptedAESKey = await encryptAESKeyWithRSA({
    key: string,
    wallet
});
</code></pre>

This encrypts the provided `AES Key` using the `RSA-OAEP` algorithm.

</details>

### Returned Data

The function call returns the following data:

```bash
{
    encryptedKey: Uint8Array,
}
```

* `encryptedKey: Uint8Array` : The `AES` key encrypted using an `RSA Public Key`.
