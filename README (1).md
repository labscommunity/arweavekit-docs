---
description: What is ArweaveKit
---

# Introduction

_**ArweaveKit aims to lower the barrier of onboarding and building on Arweave by creating a well documented one-stop library.**_

### Installing the Package

For using any functions from the library, the package must be installed in the application.

```bash
npm install arweavekit
# or
yarn add arweavekit 
```

{% hint style="success" %}
The latest stable version of ArweaveKit is <mark style="color:red;">`1.5.1`</mark>.
{% endhint %}

### Using the Library

After installation, individual functions from specific function types can be imported as follows:

<pre class="language-javascript"><code class="lang-javascript"><strong>import { createWallet } from 'arweavekit/wallet';
</strong>
const wallet = await createWallet({params});
</code></pre>

### Types of functions available&#x20;

In this library, the following types of functions are available:

* **Wallet Functions**: Functions associated with creating and using wallets. Read more [here](wallets/introduction.md).
* **Transaction Functions**: Functions associated with creating and interacting with transactions. Read more [here](transactions/introduction.md).
* **Contract Functions**: Functions associated with creating and interacting with contracts. Read more [here](broken-reference).
* **Auth Functions**: Functions associated with authentication. Read more [here](auth/introduction-to-auth.md).
* **Encryption Functions**: Functions associated with encryption. Read more [here](encryption/introduction-to-encryption.md).
* **GraphQL query functions**: Functions to query on-chain data using GraphQL. Read more [here](broken-reference).

### Compatibility

ArweaveKit is compatible with both Node.js and Browser environments. Node.js has deprecated for `v16` and suggest upgrading applications to `v18` and above, as per this [announcement](https://x.com/nodejs/status/1701309614263001569?s=20).

While ArweaveKit continues to support Node.js `v16`, a few flags must be passed in while running any scripts in order to optimally use some of ArweaveKit's latest features. If using Node.js `v16` we recommend using the following format:

```bash
node --experimental-fetch --no-warnings file-path
```

### Guide for understanding the docs

Every function has a dedicated page with the following information associated with it:

* A **brief description** of the function
* The **basic syntax** for function calls
* Any **input parameters** for the function
  * The syntax format for input parameters is `name: type`. Some parameters have the `optional` keyword which means they are optional. Parameters that do not have this keyword are required and must be passed in for successful function calls.
* The **returned data** for function calls
  * The syntax format for returned data is `name: type`. Data returned can be different different depending on the combination of input parameters used.

Links provided in data type descriptions may themselves link to other data types in cases of complex data objects. The most relevant bits have been explained throughout these docs but for a further understanding feel free to jump in to the rabbit hole.

### Example Application Ideas

Here's a list of example ideas for full-stack, end-user-facing applications you could build with `arweavekit`. These concepts leverage features of Arweave, such as decentralised data storage, pay-once store-forever pricing, transaction support, and smart contract and serverless function capabilities (using SmartWeave).

* **Decentralised Blogging Platform**: Users could write and publish blog posts that are stored permanently on Arweave. It could have an interactive frontend for easy post creation, browsing, and reading.
* **Decentralised Social Media**: A social media application where users can post text, images, and videos, create their profiles, and follow other users. All user data and interactions can be stored on Arweave.
* **Decentralised Document Collaboration**: A collaborative document editing platform that lets users create, edit, and share documents in real-time with other collaborators. It securely stores all document data on Arweave so that multiple copies are accessible and maintained indefinitely.

### Happy Building!
