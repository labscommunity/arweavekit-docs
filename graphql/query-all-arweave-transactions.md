---
description: Query GraphQL for all Arweave Transactions data iteratively
---

# Query All Arweave Transactions

You can query for all transactions on GraphQL endpoint using the method thats described here.&#x20;

### Basic Syntax

The function that we will be using is `queryAllTransactionsGQL`. For implementation details, see below.

```typescript
import { queryAllTransactionsGQL } from 'arweavekit/graphql';

const response = await queryAllTransactionsGQL(queryString, options);
```

### Input Parameters

You must supply `queryAllTransactionsGQL` with two inputs.

* `QueryString:`` `<mark style="color:red;">`string`</mark> - A valid GraphQL query string with the `first` filter.
* `Options:`` `<mark style="color:red;">`object`</mark> - An options object.
  * `gateway:`` `<mark style="color:red;">`string`</mark> - Gateway url like `arweave.net`
  * `filters:`` `<mark style="color:red;">`object`</mark> - Filters object like `first: 100`.

### Returned Data

The expected response will be a list of `GraphQLEdge`&#x20;
