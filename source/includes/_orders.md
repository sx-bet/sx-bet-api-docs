# Orders

## Get active orders

```shell
curl --location --request POST 'https://stage.api.sportx.bet/orders'
```

> The above command returns JSON structured like this

```json
{
  "status": "success",
  "data": [
    {
      "fillAmount": "0",
      "orderHash": "0xb46e5fff6498f061e93c4f5ed501ee72d924180d6aa78cdfd4d188d3383c91d4",
      "marketHash": "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
      "maker": "0x63a4491dC73245E181c47BAe0ae9d6627E56dE55",
      "totalBetSize": "10000000000000000000",
      "percentageOdds": "70455284072443640000",
      "expiry": 1631233201,
      "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
      "executor": "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
      "salt": "69415402816762328320330277846098411244657139277332120954321492419616371539163",
      "isMakerBettingOutcomeOne": true,
      "signature": "0x2aaea5b7c86166c0fbf2745c66aff794a23d21ac71ee143d08706700adbb59aa4c9b862286cf736acae5a74b10847ced73b628f4396eaab0af13b0c637fe4d021b",
      "createdAt": "2021-06-04T17:42:07.257Z"
    },
    {
      "fillAmount": "0",
      "orderHash": "0xd055d177477bd19faa9bad5cb4f907d8ebe069b614bb708713de068293cb809d",
      "marketHash": "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
      "maker": "0x63a4491dC73245E181c47BAe0ae9d6627E56dE55",
      "totalBetSize": "10000000000000000000",
      "percentageOdds": "29542732332840140000",
      "expiry": 1631233201,
      "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
      "executor": "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
      "salt": "37069036490382455296196784649228360571791475783443923366499720348790829992442",
      "isMakerBettingOutcomeOne": false,
      "signature": "0x68fb16ff440c65e0306cb16a9842da362480208a9a75597d45ca722769d93e6a13c9196a2654f764bfd5c0d4c83165c0a8ffa955ae9af8afd17544b0db29eaf71c",
      "createdAt": "2021-06-04T17:42:07.303Z"
    },
    {
      "fillAmount": "0",
      "orderHash": "0xa5a30ca2251ac1431adf3d88f5734a53b78a13b2c707211eb83996bf099e3973",
      "marketHash": "0x15c5cceb3d27518241355e9f148ef96b0a178f1bcdb366dea2d0e621a9cef1fb",
      "maker": "0x63a4491dC73245E181c47BAe0ae9d6627E56dE55",
      "totalBetSize": "10000000000000000000",
      "percentageOdds": "50000000000000000000",
      "expiry": 1631233201,
      "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
      "executor": "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
      "salt": "90344661128498016788545482097709376028896473001963632493180076229973632520043",
      "isMakerBettingOutcomeOne": true,
      "signature": "0x9b6c1e1d0cae584a3078f20d7bafd2031467a1cbce905027c6c970c13edef4357eeac625afe869417ffbecfb67b6672b765177d42fbda777f6b1a00962da2cc61c",
      "createdAt": "2021-06-04T17:42:07.270Z"
    }
  ]
}
```

This endpoint returns active orders on the exchange based on a few parameters

### HTTP Request

`POST https://stage.api.sportx.bet/orders`

### Request payload parameters

Name | Required | Type | Description
--- | --- | --- | ---

