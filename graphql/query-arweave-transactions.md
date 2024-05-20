---
description: Query GraphQL for Arweave Transactions data with pagination support
---

# Query Arweave Transactions

You can query for transactions data with support for cursor based pagination on GraphQL endpoint. It is expected from consumer of this method to write the logic for storing the cursor returned and looping until the last page.

### Basic Syntax

The function that we will be using is `queryTransactionsGQL`. For implementation details, see below.

```typescript
import { queryTransactionsGQL } from 'arweavekit/graphql';

const response = await queryTransactionsGQL(queryString, options);
```

### Input Parameters

You must supply `queryTransactionsGQL` with two inputs.

* `QueryString:`` `<mark style="color:red;">`string`</mark> - A valid GraphQL query string with `cursor` and `first` filter.
* `Options:`` `<mark style="color:red;">`object`</mark> - An options object.
  * `gateway:`` `<mark style="color:red;">`string`</mark> - Gateway url like `arweave.net`
  * `filters:`` `<mark style="color:red;">`object`</mark> - Filters object like `first: 100` . In case of no filters, pass an empty object. `cursor` filter is not optional. A persisted `cursor` filter must be supplied in the filters.

### Returned Data

The expected response will be an object with following fields.

* `status:`` `<mark style="color:green;">`number`</mark> - Query HTTP status code. Example, 200.
* `data:`` `<mark style="color:green;">`GraphQLEdge[]`</mark> - Successful response will return a list of GraphQL edges and in case of failure empty list will be returned here.
* `cursor:`` `<mark style="color:green;">`string`</mark>  - cursor id of last GraphQLEdge.
* `hasNextPage:`` `<mark style="color:green;">`boolean`</mark> - if the next page exist this will be true.
* `errors:`` `<mark style="color:green;">`GraphQLError[] | null`</mark> - Incase of failure you can expect this field to be non-nullish and a list of GraphQLError is provided.&#x20;
  * `GraphQLError:`` `<mark style="color:green;">`object`</mark> - GraphQL error object contains following fields:
    * `message:`` `<mark style="color:green;">`string`</mark> - Error message in string format
    * `extensions:`` `<mark style="color:green;">`object`</mark> - This object has a field `code` and its supposed to provide you with error code.
