---
description: Disconnecting a web wallet on Arweave
---

# Disconnect

The `disconnect` function disconnects a wallet from an applications and rescinds any provided permissions from the application.

### Basic Syntax

The function is called as follows:

```javascript
import { ArConnect } from 'arweavekit/auth'

const response = await ArConnect.disconnect();
```
