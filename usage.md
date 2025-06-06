# Usage

Below is a quick example of how to initialize the Arweave Data Storage SDK,create a drive, a folder, and a file, or quickly upload a file. For more detailed use-cases, refer to the [Examples](https://github.com/) section.

#### Basic Setup

To use the SDK, initialize StorageApi with a configuration object. This will create a new Arweave Data Storage SDK client. You may also specify the application name (`appName`) and optional configurations.

```
const { Configuration, StorageApi, Token, Network } = require('arweave-storage-sdk');

const config = new Configuration({
	appName: '<Name of your App>'
	privateKey: '<ENV to private key or use_web_wallet>',
	network: Network.BASE_MAINNET,
	token: Token.USDC
})

const storageClient = new StorageApi(config);
await storageApiInstance.ready
```

#### Authentication

Once you have the storage client initialized and before you go ahead to upload any files, its really important to create a secured session by authenticating yourself. This allows you to track or query your uploads, receipts. It is easy and can be done in one line.

```
  //Login
  await storageApiInstance.api.login()
```

And that's it. You’re ready to make authenticated requests with the service.

#### Upload cost estimates

Assuming you have a valid session post login, the next step is to query for file upload prices. This is an optional step, in-case you are interested in setting up uploads conditionally or to check your wallet for enough balance before your upload. Based on your selected token and network, estimates will be provided to you in the same token and also in USD.

```
export interface GetEstimatesResponse {
  size: number
  usd: number
  usdc: {
    amount: string
    amountInSubUnits: string
  }
  payAddress: string
}
const size = file.size // 200000 bytes
const estimates = await storageClient.getEstimates(size) // size of type number

console.log(estimates)
{ 
  "data": { 
"size": 200000, 
"usd": 0.008599242237052303, 
"usdc": { 
"amount": "0.0086", 
"amountInSubUnits": "8600" 
}, 
"payAddress": "<USDC ADDRESS OF THE SERVICE>" 
  } 
}
```

#### Quick file upload

Upload a file (or buffer) quickly using the quickUpload method.

The `quickUpload` method simplifies the process of uploading a file to Arweave. It automatically handles the creation of the transaction, including setting metadata such as content type, visibility, and tags. The receipt returned includes the unique ID, to query and confirm the file upload.

```
const file = <web File object, file path, buffer or stream>�const receipt = await storageClient.quickUpload(file, {
	name: file.name || "test.txt",
	dataContentType: 'text/plain', // content type of the file
	visibility: '<public|private>',
	tags: [{name: "Collection-Type", value: "ART"}],�	size: file.size // size in bytes of type number
});

console.log('File has been uploaded. receipt:', receipt.id);
```

#### Creating a Drive

Create a new drive to manage your files on Arweave.

Drives act as containers for your files and folders. The additional parameters such as visibility and tags help you categorize and control access to your content. This context is useful if you’re new to managing storage on decentralized platforms.

```
const drive = await storageClient.drive.create('My Drive', { 
visibility: 'public',
tags: [{name: "Collection-Type", value: "ART"}] 
});

console.log('Drive created with ID:', drive.id);
```

#### Creating a Folder

Organize your files by creating folders within a drive.

Folders help you structure your files within a drive. In this example, you can see how to specify the parent drive and (optionally) a parent folder to build a hierarchical file system.

```
const folder = await storageClient.folder.create('My Folder', {
driveId: '<driveId>',
parentFolderId: '<parentFolderId>',
visibility: 'public',
tags: [{name: "Collection-Type", value: "ART"}]
});

console.log('Folder created with ID:', folder.id);
```

#### Creating a File

Store a file on Arweave by creating a file transaction.

This snippet creates a file by converting a string into a buffer and then sending it as a transaction to Arweave. The parameters include metadata like file name, size, and content type.

```
const fileData = Buffer.from('Hello, Arweave!');

const file = await storageClient.file.create({
	name: 'My File',
	size: fileData.length,
	dataContentType: 'text/plain',
	driveId: '<driveId>',
	parentFolderId: '<parentFolderId>',
	file: fileData,
	visibility: 'public',
	tags: [{name: "Collection-Type", value: "ART"}]
});

console.log('File uploaded; transaction ID:', file.txId);
```

_Note: The `visibility` field can be set to `public` or `private`._
