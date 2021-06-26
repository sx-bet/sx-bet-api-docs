# Metadata

## Get metadata

```shell
curl --location --request GET 'https://app.api.sportx.bet/metadata'
```

> The above command returns JSON structured like this

```json
{
  "status": "success",
  "data": {
    "executorAddress": "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
    "oracleFees": {
      "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063": "4000000000000000000",
      "0x7ceB23fD6bC0adD59E62ac25578270cFf1b9f619": "4000000000000000000",
      "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174": "4000000000000000000"
    },
    "sportXAffiliate": {
      "address": "0xA216136Ac816FC1E816af5FffDC9E58281e14383",
      "amount": "0"
    },
    "makerOrderMinimums": {
      "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063": "10000000000000000000",
      "0x7ceB23fD6bC0adD59E62ac25578270cFf1b9f619": "5000000000000000",
      "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174": "10000000"
    },
    "takerMinimums": {
      "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063": "5000000000000000000",
      "0x7ceB23fD6bC0adD59E62ac25578270cFf1b9f619": "2500000000000000",
      "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174": "5000000"
    },
    "addresses": {
      "1": {
        "DAI": "0x6B175474E89094C44Da98b954EedeAC495271d0F",
        "SX": "0x99fE3B1391503A1bC1788051347A1324bff41452",
        "USDC": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48"
      },
      "137": {
        "DAI": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
        "WETH": "0x7ceB23fD6bC0adD59E62ac25578270cFf1b9f619",
        "USDC": "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174"
      }
    },
    "bettingEnabled": true,
    "depositMinimums": {
      "0x6B175474E89094C44Da98b954EedeAC495271d0F": "100000000000000000000",
      "0x99fE3B1391503A1bC1788051347A1324bff41452": "500000000000000000000",
      "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48": "100000000"
    },
    "withdrawMinimums": {
      "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063": "100000000000000000000",
      "0x7ceB23fD6bC0adD59E62ac25578270cFf1b9f619": "100000000000000000",
      "0x840195888Db4D6A99ED9F73FcD3B225Bb3cB1A79": "500000000000000000000",
      "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174": "100000000"
    },
    "totalVolume": 11098310.470151696
  }
}
```

This endpoint retrieves metadata on the exchange itself and useful parameters to interact with the exchange.

### HTTP Request

`GET https://app.api.sportx.bet/metadata`

### Response format

| Name               | Type    | Description                                                                                                                                                           |
| ------------------ | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| status             | string  | `success` or `failure` if the request succeeded or not                                                                                                                |
| data               | any     | The metadata for the exchange                                                                                                                                         |
| executorAddress    | string  | The executor address for the sportx.bet exchange. Use this address for setting the `executor` when posting new orders as a market maker                               |
| oracleFees         | any     | A mapping from token address to a percentage indicating the fees paid on profit for each token. To convert to a readable number, divide by 10^20                      |
| sportXAffiliate    | any     | The default sportx.bet affiliate. Currently set to 0 and unused                                                                                                       |
| makerOrderMinimums | any     | A mapping from token address to a real token amount indicating the minimum maker order size.                                                                          |
| takerMinimums      | any     | A mapping from token address to a real token amount indicating the minimum taker order size                                                                           |
| addresses          | any     | A mapping from network id -> canonical token name -> token address of assets supported by the exchange                                                                |
| bettingEnabled     | boolean | `true` if betting is enabled for your region, false otherwise. See [here](https://help.sportx.bet/en/articles/3613372-terms-and-conditions) for the supported regions |
| depositMinimums    | any     | A mapping from token address to real token amount indicating the minimum amount required to bridge from Ethereum mainnet to Polygon                                   |
| withdrawMinimums   | any     | A mapping from token address to real token amount indicating the minimum amount required to bridge from Polygon to Ethereum mainnet                                   |
| totalVolume        | number  | All time total volume on the exchange                                                                                                                                 |

<aside class="notice">
To convert the <code>makerOrderMinimums</code> into a readable token amount, divide by 10^18 for all baseTokens other than USDC. For USDC divide by 10^6.
</aside>

<aside class="notice">
To convert the <code>takerMinimums</code> into a readable token amount, divide by 10^18 for all baseTokens other than USDC. For USDC divide by 10^6.
</aside>
