---
description: Plug in a external package to arweavekit/wallet
---

# Wallet Plugins

The `use` function exposed via the ArweaveKit object from `arweavekit/wallet` package allows you to plugin external packages into arweave kit package.

### Basic Syntax

The function is called as follows:

{% code title="usage.js" %}
```javascript
import * as externalPackage from 'externalPackage';
import { ArweaveKit } from 'arweavekit/wallet';

const arweaveKit = ArweaveKit.use({ name: 'MyPlugIn', plugin: externalPackage });

console.log(arweavekit.functionFromExternalPackage())
```
{% endcode %}



{% hint style="info" %}
The ArweaveKit object imported also contains all functions from the ArweaveKit package for ease of use.
{% endhint %}

### Create a Plugin

Most existing packages in Arweave will already be supported without any additional work, the functions just need to be defined and exported in the external package:

{% code title="externalPackage.js" %}
```javascript
import * as ExternalPackage from 'package'
export function PackagePlugIn() {
    return ExternalPackage
}
```
{% endcode %}
