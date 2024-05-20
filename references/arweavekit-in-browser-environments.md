---
description: Sample configurations needed for using ArweaveKit in Browser Environments
---

# ArweaveKit in Browser Environments

In today's web development landscape, module bundlers and frameworks play a pivotal role in optimizing and deploying code for browser environments. Despite their numerous advantages, it's important to note that these bundlers often require separate polyfill configurations to ensure support for Node's [Core Modules](https://nodejs.org/dist/latest-v16.x/docs/api/modules.html#core-modules) across different browsers.

### NextJS

NextJS is compatible with ArweaveKit out of the box and does not require separate polyfills for the modules.

### NuxtJS

Nuxt 3 requires the implementation of polyfills in order to use the core modules in browser environments. Since Nuxt ships with Vite by default, we can use the Vite plugin for the same.

#### Setup

Here's a sample setup to successfully polyfill required modules and use the functionality from arweavekit in a Nuxt app.

The first step is installing the dependency:

```bash
npm install --save-dev vite-plugin-node-polyfills
# or
yarn add --dev vite-plugin-node-polyfills
```

Then this polyfill plugin must be added to the `nuxt.config.ts` file and the nuxt config should look similar to the config below:

{% code title="nuxt.config.ts" %}
```javascript
import { nodePolyfills } from "vite-plugin-node-polyfills";

export default defineNuxtConfig({
  // other configs
  vite: {
    plugins: [
      nodePolyfills({
        include: ["buffer", "crypto", "stream", "util", "vm"],
        globals: {
          process: false,
        },
      }),
    ],
    resolve: {
      alias: [
        {
          find: "ethers",
          replacement:
            "https://cdnjs.cloudflare.com/ajax/libs/ethers/6.7.0/ethers.min.js",
        },
      ],
    },
  },
});

```
{% endcode %}

{% hint style="warning" %}
This is a sample config. For more advanced options visit [here](https://github.com/davidmyersdev/vite-plugin-node-polyfills).
{% endhint %}

Now, add arweavekit plugin named `arweavekit.client.ts` to the `plugins` directory in the root directory of the nuxt project. And, import and return the essential functions from arweavekit in this plugin.

{% code title="arweavekit.client.ts" %}
```typescript
import {
  createTransaction,
  signTransaction,
  postTransaction,
  queryAllTransactionsGQL,
  createContract,
  writeContract,
} from "arweavekit";

export default defineNuxtPlugin(() => {
  return {
    provide: {
      createTransaction,
      signTransaction,
      postTransaction,
      queryAllTransactionsGQL,
      createContract,
      writeContract,
    },
  };
});

```
{% endcode %}

Now, you can use the functions from this plugin in your vue files as below.

{% code title="app.vue" %}
```tsx
<script setup lang="ts">
const {
  $createTransaction: createTransaction,
  $signTransaction: signTransaction,
  $postTransaction: postTransaction,
  $queryAllTransactionsGQL: queryAllTransactionsGQL,
  $createContract: createContract,
  $writeContract: writeContract,
} = useNuxtApp();

// An example function to write to a contract in testnet
async function writeContractTestNet() {
  const response = await writeContract({
    environment: "testnet",
    contractTxId: "CO7NkmEVj4wEwPySxYUY0_ElrEqU4IeTglU2IilCnLA",
    options: {
      function: "increment",
    },
  });
  console.log(response);
}
</script>

<template>
  <div class="container mx-auto flex justify-center h-screen pt-12">
    <div class="flex flex-col gap-4 w-1/2">
      <button class="border-4" @click="writeContractTestNet">
        Write Contract Testnet
      </button>
    </div>
  </div>
</template>
```
{% endcode %}

### Vite

In an attempt to prevent runtime errors, Vite produces [errors](https://github.com/vitejs/vite/issues/9200) or [warnings](https://github.com/vitejs/vite/pull/9837) when your code references built-in modules such as `fs` or `path`. These must be polyfilled separately to utilize the core modules in browser environments.

#### Setup

Here's a sample setup to successfully polyfill required modules in a Vite app.

The first step is installing the dependency:

```bash
npm install --save-dev vite-plugin-node-polyfills
# or
yarn add --dev vite-plugin-node-polyfills
```

Then the plugin must be added to the `vite.config.js` file:

```javascript
import { defineConfig } from 'vite'
import { nodePolyfills } from 'vite-plugin-node-polyfills'

// https://vitejs.dev/config/
export default defineConfig({
  // other configs
  plugins: [
    // other plugins
    nodePolyfills({
        include: ["buffer", "crypto", "stream", "util", "http"],
    }),
  ],
})
```

{% hint style="warning" %}
This is a sample config. For more advanced options visit [here](https://github.com/davidmyersdev/vite-plugin-node-polyfills).
{% endhint %}

{% hint style="info" %}
This config is compatible with all Vite-supported frameworks. Read more about the supported frameworks [here](https://vitejs.dev/guide/).
{% endhint %}

### Webpack

Webpack versions < 5 used to include polyfills by default, however, this must be implemented separately for Webpack versions > 5 in order to use the core modules in browser environments.

#### Setup

Here's a sample setup to successfully polyfill required modules in an app using Webpack as a bundler.

The first step is installing the dependency:

```bash
npm install --save-dev @craco/craco node-polyfill-webpack-plugin
# or
yarn add --dev @craco/craco node-polyfill-webpack-plugin
```

Then the setups must be added to a `craco.config.js` file:

```javascript
const NodePolyfillPlugin = require("node-polyfill-webpack-plugin");

module.exports = {
  webpack: {
    // Using craco to import files from outside the src/ directory
    configure: (webpackConfig) => {
      const scopePluginIndex = webpackConfig.resolve.plugins.findIndex(
        ({ constructor }) =>
          constructor && constructor.name === "ModuleScopePlugin"
      );

      webpackConfig.resolve.plugins.splice(scopePluginIndex, 1);
      return webpackConfig;
    },
    plugins: {
      add: [
        new NodePolyfillPlugin({
          includeAliases: ["buffer", "Buffer", "crypto", "stream"],
        }),
      ],
    },
  },
};
```

And finally, replace the default scripts in `package.json` as follows:

```json
"scripts": {
    "start": "craco start",
    "build": "craco build",
    "test": "craco test",
    "eject": "react-scripts eject"
}
```

{% hint style="warning" %}
This is a sample config. For more advanced options visit [here](https://www.npmjs.com/package/node-polyfill-webpack-plugin).
{% endhint %}

{% hint style="info" %}
This config is compatible with React applications. Learn more about React applications [here](https://create-react-app.dev/).
{% endhint %}
