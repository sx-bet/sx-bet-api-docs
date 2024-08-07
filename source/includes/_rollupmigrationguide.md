# SX Rollup Migration Guide

## What is this migration?

The current version of SX Network was built on the Polygon Edge SDK. This project has since been discontinued, and so there is no support or improvements coming for the chain. For a number of reasons including improving block times, making use of a canonical bridge, better stability and developer support, we have decided to migrate our chain to an Arbitrum Orbit Rollup chain.

You can read more about the rationale [here](https://medium.com/sportx-bet/sx-rollup-ca33079d1b8b).

<aside class="notice">
For the purposes of this migration, we will refer to current (legacy) chain as SXN and the new chain as SXR.
</aside>

## What do I have to do?

When the sport you're interested in has moved over to **SXR**, you'll have to:

- Update token addresses for `USDC` and `WSX` with the new token addresses
- Update rest API calls as shown [here](#endpoint-changes)
- Update websocket streams handlers for orders, trades, and markets *(they will now include `chainVersion`)*
- Migrate funds from **SXN** to **SXR** using our bridge
- Configure the payloads with the new `chainId`, `domainVersion` and other configs found [here](#references) and/or [here](#metadata)
- If you are [filling orders programattically ](#filling-orders), you must change the contract ABI (two new fields under FillObject type)
- Reenable betting for each token as described [here](#enabling-betting)
- Start using API as normal for **SXR** Markets

## Endpoint Changes

The following endpoints allow a new query parameter: `chainVersion`. This will filter the API response to only the specific chain you are looking for. If no parameter is passed, there is a non-intrusive default used.

<aside class="warning">
When `chainVersion` is empty for GET requests, the result will show data for both chains.
</aside>
<aside class="warning">
When `chainVersion` is empty for POST requests, the default data is for SXN chain.
</aside>

This ensures the changes are least disruptive, and changes are only required when handling games on the new chain.

**Allowed values for `chainVersion` are:**

| `chainVersion` | Description       |
| -------------- | ----------------- |
| SXN            | Legacy SX Network |
| SXR            | SX Rollup         |


### SXR Metadata
#### Get SXR Metadata
`GET https://api.sx.bet/metadata?chainVersion=SXR`
### SXR Leagues
#### Get Active SXR Leagues
`GET https://api.sx.bet/leagues/active?chainVersion=SXR`
### SXR Markets
#### Get Active SXR Markets
`GET https://api.sx.bet/markets/active?chainVersion=SXR`
#### Get Popular SXR Markets
`GET https://api.sx.bet/markets/popular?chainVersion=SXR`
### SXR Trades
#### Get SXR Trades
`GET https://api.sx.bet/trades?chainVersion=SXR`
### SXR Consolidated Trades
#### Get SXR Consolidated Trades
`GET https://api.sx.bet/trades/consolidated?chainVersion=SXR`
### SXR Orders
#### Get SXR Orders
`GET https://api.sx.bet/orders?chainVersion=SXR`
#### Cancel SXR Orders
`POST https://api.sx.bet/orders/cancel/v2?chainVersion=SXR`
#### Cancel SXR Orders by Event
`POST https://api.sx.bet/orders/cancel/event?chainVersion=SXR`
#### Cancel all SXR Orders
`POST https://api.sx.bet/orders/cancel/all?chainVersion=SXR`

## Sport Migration Schedule

Our plan is to migrate by sport to reduce impact as much as possible. Our migration by sport schedule is as follows:

| Sport(s)                                                                        | Date           |
| ------------------------------------------------------------------------------- | -------------- |
| E Sports, Novelty Markets, Rugby, Politics, Entertainment, NFTs, Daily Parlays  | July 29, 2024  |
| Boxing, Olympics, Racing, Cricket                                               | July 30, 2024  |
| Football, Hockey, Basketball                                                    | July 31, 2024  |
| Baseball, Golf, Soccer, Tennis, Mixed Martial Arts                              | August 5, 2024 |
| Crypto, Degen Crypto                                                            | August 6, 2024 |
