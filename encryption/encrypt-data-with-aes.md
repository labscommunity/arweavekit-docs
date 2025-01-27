---
description: Encrypt Data with the Advanced Encryption Standard (AES)
---

# Encrypt Data with AES

The `encryptDataWithAES` performs symmetric encryption using the [Advanced Encryption Standard (AES)](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt#aes-gcm), specifically the Galois/ Counter Mode (GCM). Symmetric encryption is optimal for data encryption and performs the encryption and decryption of data with a single key.

A new `AES` key is generated each time the function is called. The data is encrypted using this key and a randomly generated initialized vector (`iv`).&#x20;

The `iv` is required for decryption as well, hence it is returned prepended to the encrypted data as a combined `Array Buffer`. The encryption key is returned as well, as part of the return object. The key is generated as a `CryptoKey object` however it is converted to a `base64` encoded `string` before being returned.

### Basic Syntax

The function is called as follows:

```javascript
import { encryptDataWithAES } from 'arweavekit/encryption';

const encryptedDataObject = await encryptDataWithAES({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `data: ArrayBuffer` : The data to be encrypted passed in as an `ArrayBuffer`. The `ArrayBuffer` is optimal for data encryption using `AES-GCM` and is one of the preferred types for uploading data on Arweave.

<details>

<summary>Example</summary>

```javascript
const encryptedDataObject = await encryptDataWithAES({
    data: ArrayBuffer,
});
```

This encrypts the provided `ArrayBuffer` using the `AES-GCM` encryption method.

</details>

### Returned Data

The function call returns the following data:

```bash
{
    rawEncryptedKeyAsBase64: Base64 string,
    combinedArrayBuffer: ArrayBuffer,
}
```

* `rawEncryptedKeyAsBase64: string` : The encryption key generated at the time of data encryption using `AES-GCM` and encoded using `Base64` format.
* `combinedArrayBuffer: ArrayBuffer` : The combination of the random initialized vector prepended to the encrypted data as an `ArrayBuffer`.
