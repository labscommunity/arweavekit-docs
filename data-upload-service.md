# Data Upload Service

This service is used with Arweave Data Storage SDK to upload data to Arweave and pay for the storage using other chain's stablecoin tokens.

Supported chains and stablecoins:

Ethereum and EVM: USDC and USDT

Solana: USDC and USDT

Cosmos: Noble

### Prerequisites

* Docker
* Node.js (>= v20.18.3)
* pnpm (>= v9.14.2)

### Installation

```
pnpm install
```

### Running the service

```
pnpm start:dev
```

### Running the service in production mode

```
pnpm start:prod
```

### Prisma migrations

```
pnpm db:migrate:dev
```

```
pnpm db:migrate:prod
```

### Prisma Studio

```
pnpm db:studio

```

