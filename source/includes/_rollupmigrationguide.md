# SX Rollup Migration Guide

## What is this migration and why are we migrating?

The current version of SX Network was built on the Polygon Edge SDK. This project has since been discontinued, and so there is no support or improvements coming for the chain. For a number of reasons including improving block times, making use of a canonical bridge, better stability and developer support, we have decided to migrate our chain to an Arbitrum Orbit Rollup chain.

You can read more about the rationale [here](https://medium.com/sportx-bet/sx-rollup-ca33079d1b8b).

## How will the migration affect betting?

Our plan is to migrate by sport to reduce impact as much as possible. Our migration by sport schedule is as follows:

| Sport(s)        | Date        |
| --------------- | ----------- |
| Sport1, Sport2  | Aug 1, 2024 |
| Sport3          | Aug 8, 2024 |

## Endpoints

The following endpoints allow a new query parameter: `chainVersion`. This will filter out response to only the specific chain you are looking for. If no parameter is passed, the data will return for both chains.

Allowed values for `chainVersion` are:

| `chainVersion` | Description       |
| -------------- | ----------------- |
| SXN            | Legacy SX Network |
| SXR            | SX Rollup         |

<aside class="warning">
WHEN `chainVersion` IS EMPTY FOR GET REQUESTS, RESULT WILL SHOW DATA FOR BOTH CHAINS.
</aside>
<aside class="warning">
WHEN `chainVersion` IS EMPTY FOR POST REQUESTS, WE DEFAULT TO SXN.
</aside>

This ensures the changes are least disruptive, and changes are only required when handling games on the new chain.

### Metadata

`GET https://api.sx.bet/metadata?chainVersion=SXR`

### Leagues

`GET https://api.sx.bet/leagues/active?chainVersion=SXR


### Markets

`GET https://api.sx.bet/markets/active?chainVersion=SXR`
`GET https://api.sx.bet/markets/popular?chainVersion=SXR`

### Trades

`GET https://api.sx.bet/trades?chainVersion=SXR`

### Consolidated Trades

`GET https://api.sx.bet/trades/consolidated?chainVersion=SXR`

### Orders

`GET https://api.sx.bet/orders?chainVersion=SXR`
`POST https://api.sx.bet/orders/new?chainVersion=SXR`
`POST https://api.sx.bet/orders/cancel/v2?chainVersion=SXR`
`POST https://api.sx.bet/orders/cancel/event?chainVersion=SXR`
`POST https://api.sx.bet/orders/cancel/all?chainVersion=SXR`