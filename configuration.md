# Configuration

Initialize the **Arweave Data Storage SDK** object with various configuration options. The `appName` is recommended as it helps in organizing and searching your transactions on Arweave. The `privateKey` can either be your account’s key or a flag to use a browser wallet. Other parameters like `network`, `token`, and `gateway` let you tailor the SDK to your specific environment.

```
const { Configuration, Network, Token} = require('arweave-storage-sdk');

const config = new Configuration({
	appName: 'My cool project'
	privateKey: process.env.PRIVATE_KEY,
	network: Network.BASE_MAINNET,
	token: Token.USDC
})
```

| Option       | Optional | Description                                                                                                                                          |
| ------------ | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `appName`    | true     | App name to be used in Arweave transactions. Recommended to use since it makes searching all your app files easier.                                  |
| `privateKey` | false    | Private key of your account. JWK in case of Arweave. if `'use_web_wallet'` is used, sdk will rely on browser wallets.                                |
| `network`    | true     | Network of your payment token. Eg: 'SOL\_MAINNET'. Simply use the Network object provided by the sdk to see supported networks. Defaults to Arweave. |
| `token`      | true     | Token to use for payments. Eg: 'USDT'. Use the Token object provided by the sdk to see all supported tokens. Defaults to AR.                         |

* **Encryption:** For private drives or file storage, use the built-in Crypto utilities to manage encryption.
* **API Calls:** The SDK uses the ArFSApi internally to interact with the Arweave network. You can override or customize gateway endpoints if needed.
