---
description: Decrypt Data with the Advanced Encryption Standard (AES)
---

# Decrypt Data with AES

The `decryptDatawithAES` performs symmetric encryption using the [Advanced Encryption Standard (AES)](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt#aes-gcm), specifically the Galois/ Counter Mode (GCM).

The `AES` key and the random initialized vector (`iv`) used at the time of encryption are needed to decrypt the data.

The `iv` is part of the `combinedArrayBuffer` returned as the encrypted data from the `encryptDataWithAES` function. The `decryptDataWithAES` functions splits this into the `iv` and actual `encryptedData` on the backend before decrypting the latter.

### Basic Syntax

The function is called as follows:

```javascript
import { decryptDatawithAES } from 'arweavekit/encryption';

const decryptedDataObject = await decryptDatawithAES({params});
```

### Input Parameters

The following params are available for this function and they must be passed in as an object:

* `data: ArrayBuffer` : The combination of the random initialized vector prepended to the encrypted data as an `ArrayBuffer` generated at the time of encryption.
* `key: string` : The encryption key generated at the time of data encryption using `AES-GCM` and used for encrypting the data.

<details>

<summary>Example</summary>

```javascript
const decryptedDataObject = await decryptDatawithAES({
    data: ArrayBuffer,
    key: string,
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

* `decryptedData: ArrayBuffer` : The decrypted data returned as an `ArrayBuffer`.
