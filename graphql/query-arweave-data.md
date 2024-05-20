---
description: Query GraphQL for Arweave Blocks and Transactions data
---

# Query Arweave Data

You can query for everything that Arweave GraphQL endpoint supports. For instance, single transaction, more than one transaction, single block, more than one block.

### Basic Syntax

The function that we will be using is `queryGQL`. For implementation details, see below.

```typescript
import { queryGQL } from 'arweavekit/graphql';

const response = await queryGQL(queryString, options);
```

### Input Parameters

You must supply `queryGQL` with two inputs.

* `QueryString:`` `<mark style="color:red;">`string`</mark> - A valid GraphQL query string.
* `Options:`` `<mark style="color:red;">`object`</mark> - An options object.
  * `gateway:`` `<mark style="color:red;">`string`</mark> - Gateway url like `arweave.net`
  * `filters:`` `<mark style="color:red;">`object`</mark> - Filters object like `first: 100` . In case of no filters, pass an empty object.

### Returned Data

The expected response will be an object with following fields.

* `status:`` `<mark style="color:green;">`number`</mark> - Query HTTP status code. Example, 200.
* `data:`` `<mark style="color:green;">`object | null`</mark> - Successful response will return GraphQL node or list of GraphQL edges and in case of failure null will be returned here.
* `errors:`` `<mark style="color:green;">`GraphQLError[] | null`</mark> - Incase of failure you can expect this field to be non-nullish and a list of GraphQLError is provided.&#x20;
  * `GraphQLError:`` `<mark style="color:green;">`object`</mark> - GraphQL error object contains following fields:
    * `message:`` `<mark style="color:green;">`string`</mark> - Error message in string format
    * `extensions:`` `<mark style="color:green;">`object`</mark> - This object has a field `code` and its supposed to provide you with error code.
