---
description: Apply various customizations to the Wallet Kit UI
---

# Customization

## Manage customizations

Custom configuration can be applied using the Wallet Kit Provider:

```tsx
...
   <ArweaveWalletKit
      theme={{
        displayTheme: "light",
        accent: {
          r: 0,
          g: 0,
          b: 0
        },
        titleHighlight: {
          r: 0,
          g: 122,
          b: 255
        },
        radius: "default"
      }}
      config={{
        strategies: [
          new ArConnectStrategy(),
          new WebWalletStrategy(),
          new OthentStrategy(),
          new BrowserWalletStrategy()
        ],
        permissions: ["ACCESS_ADDRESS", "ACCESS_ALL_ADDRESSES"],
        ensurePermissions: true,
        appInfo: {
          name: "Test App",
          logo: "https://arweave.net/tQUcL4wlNj_NED2VjUGUhfCTJ6pDN9P0e3CbnHo3vUE"
        },
        gatewayConfig: {
          host: "arweave.net",
          port: 443,
          protocol: "https"
        }
      }}
    >
    <YourApp />
  </ArweaveWalletKit>
...
```

## Application info

Using the `config` field of the [`<ArweaveWalletKit>`](setup.md#setup-provider) provider component, you can define a name, a logo or the required permissions for your app. The following options are available:

| Prop                | Type                                                                                  | Default             | Description                                                                                                |
| ------------------- | ------------------------------------------------------------------------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------- |
| `permissions`       | [`PermissionType[]`](https://docs.arconnect.io/api/connect#permissions)               | `[]`                | Permissions to connect with.                                                                               |
| `ensurePermissions` | `boolean`                                                                             |  `false`            | Ensure that all required permissions are present. If false, it only checks if the app has any permissions. |
| `appInfo`           | [`AppInfo`](https://docs.arconnect.io/api/connect#additional-application-information) | `{}`                | Information about your app (name/logo).                                                                    |
| `gatewayConfig`     | [`GatewayConfig`](https://docs.arconnect.io/api/connect#custom-gateway-config)        | arweave.net gateway | Configuration for the Arweave gateway to use.                                                              |

## Theming

With the `theme` field, you can define a custom theme configuration for the Arweave Wallet Kit modals and buttons. The following options are available:

| Prop             | Type                               | Description                                                            |
| ---------------- | ---------------------------------- | ---------------------------------------------------------------------- |
| `displayTheme`   | `"dark"`, `"light"`                | UI display theme to use                                                |
| `accent`         | `RGBObject`                        | RGB accent color for the UI                                            |
| `titleHighlight` | `RGBObject`                        | RGB accent color for the subscreen titles (like the connection screen) |
| `radius`         | `"default"`, `"minimal"`, `"none"` | Border radius level used throughout the Kit UI                         |
