---
description: Checks for injected web wallet
---

# Is Installed

The `isInstalled` function checks if the ArConnect global object (extension) is injected into the application. Else it points to the installation page for the same.

### Basic Syntax

The function is called as follows:

```javascript
import { ArConnect } from 'arweavekit/auth'

const response = await ArConnect.isInstalled();
```
