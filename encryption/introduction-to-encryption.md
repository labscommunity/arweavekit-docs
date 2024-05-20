---
description: Introduction to encryption and decryption on Arweave
---

# Introduction to Encryption

### Need for encryption

Arweave has brought forth the ability to "permanently" store data at a low cost leveraging the benefits of decentralization.

Arising from the benefits of immutability and openness, however, is a need to ensure adequate data protection for sensitive and private information.

With the help of encryption and decryption features, users can seek the benefits of permanent data storage and rest assured that their data is confidential and secure.

### How does encryption work?

On a high level, data that must be secured, is locked cryptographically and the key for unlocking it is only provided to the user that encrypts this information. This ensures that only the user encrypting the data can securely decrypt and access it again.

### Encryption from a development perspective

Developers can create user interfaces for users to securely encrypt and decrypt their data easily.&#x20;

{% hint style="danger" %}
It is important that developers handle the process with end-to-end encryption, where in no one (including the developers), except the end user has access to the keys.
{% endhint %}

### Tools used

The functions associated with smart contracts leverage the following tools:

* [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web\_Crypto\_API)
* [Arweave Wallet (Window Object)](https://docs.arconnect.io/api/intro)

### Encryption based functions

In this section, we will look at the following features:

* encrypt data with AES
* decrypt data with AES
* encrypt AES key with RSA
* decrypt AES key with RSA
