# Data Upload Service

This service is used with Arweave Data Storage SDK to upload data to Arweave and pay for the storage using other chain's stablecoin tokens.

_**Supported chains and stablecoins**_

_Ethereum and EVM:_ USDC and USDT

_Solana:_ USDC and USDT

_Cosmos:_ Noble

_If you would like to request support for a stablecoin payment on a different chain, please open an issue in the github repo_ [_here_](data-upload-service.md)

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

