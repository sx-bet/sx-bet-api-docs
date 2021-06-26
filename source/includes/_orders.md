# Orders

## Get active orders

```shell
curl --location --request POST 'https://app.api.sportx.bet/orders'
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

`POST https://app.api.sportx.bet/orders`

### Request payload parameters

| Name         | Required | Type     | Description                                    |
| ------------ | -------- | -------- | ---------------------------------------------- |
| marketHashes | false    | string[] | Only get orders for these market hashes        |
| baseToken    | false    | string   | Only get orders denominated in this base token |
| maker        | false    | string   | Only get orders for this market maker          |

### Response format

| Name                     | Type    | Description                                                                                                                                                                                                                                                                          |
| ------------------------ | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| fillAmount               | string  | How much this order has been filled in Ethereum units up to a max of `totalBetSize`. To get a human readable amount, divide by either 10^18 for DAI and ETH or 10^6 for USDC.                                                                                                        |
| orderHash                | string  | A unique identifier for this order                                                                                                                                                                                                                                                   |
| marketHash               | string  | The market corresponding to this order                                                                                                                                                                                                                                               |
| maker                    | string  | The market maker for this order                                                                                                                                                                                                                                                      |
| totalBetSize             | string  | The total size of this order in Ethereum units. To get a human readable amount, divide by either 10^18 for DAI and ETH or 10^6 for USDC.                                                                                                                                             |
| percentageOdds           | string  | The odds that the `maker` receives in the sportx protocol format. To convert to an implied percentage odds divide by 10^20. To convert to the odds that the taker would receive if this order would be filled in implied format, use the formula `takerOdds=1-percentageOdds/10^20`. See the [unit conversion section](#odds-display-on-sportx) for more details. |
| expiry                   | number  | The time in unix seconds after which this order is no longer valid                                                                                                                                                                                                                   |
| baseToken                | string  | The base token this order is denominated in                                                                                                                                                                                                                                          |
| executor                 | string  | The address permitted to execute on this order. This is set to the sportx.bet exchange                                                                                                                                                                                               |
| salt                     | string  | A random number to differentiate identical orders                                                                                                                                                                                                                                    |
| isMakerBettingOutcomeOne | boolean | `true` if the maker is betting outcome one (and hence taker is betting outcome two if filled)                                                                                                                                                                                        |
| signature                | string  | Signature of the maker on this order                                                                                                                                                                                                                                                 |

## Post a new order

```shell
curl --location --request POST 'https://app.api.sportx.bet/orders/new' \
--header 'Content-Type: application/json' \
--data-raw '{
    "orders": [
        {
            "marketHash": "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
            "maker": "0x6F75bA6c90E3da79b7ACAfc0fb9cf3968aa4ee39",
            "totalBetSize": "21600000000000000000",
            "percentageOdds": "47846889952153115000",
            "baseToken": "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
            "expiry": "1631233201",
            "executor": "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
            "isMakerBettingOutcomeOne": true,
            "signature": "0x50b00e7994b0656f78701537296444bccba2a7e4d46a84ff26c8ca48cb66774c76faa893be293412959779900232065c8236e489158070777d7a3e1a37d911811b",
            "salt": "61882422358902283358380622686147595792242782952753619716150366288606659190035"
        }
    ]
}'
```

```javascript
import { BigNumber, utils, providers, Wallet } from "ethers";

const order = {
  marketHash:
    "0x0eeace4a9bbf6235bc59695258a419ed3a05a2c8e3b6a58fb71a0d9e6b031c2b",
  maker: "0x6F75bA6c90E3da79b7ACAfc0fb9cf3968aa4ee39",
  totalBetSize: BigNumber.from("21600000000000000000"),
  percentageOdds: BigNumber.from("47846889952153115000"),
  baseToken: "0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063",
  expiry: BigNumber.from(1631233201),
  executor: "0x3E91041b9e60C7275f8296b8B0a97141e6442d49",
  isMakerBettingOutcomeOne: true,
  salt: BigNumber.from(utils.randomBytes(32)),
};

const orderHash = utils.arrayify(
  utils.solidityKeccak256(
    [
      "bytes32",
      "address",
      "uint256",
      "uint256",
      "uint256",
      "uint256",
      "address",
      "address",
      "bool",
    ],
    [
      order.marketHash,
      order.baseToken,
      order.totalBetSize,
      order.percentageOdds,
      order.expiry,
      order.salt,
      order.maker,
      order.executor,
      order.isMakerBettingOutcomeOne,
    ]
  )
);

// Example shown here with an ethers.js wallet if you're interacting with the exchange using a private key
const wallet = new Wallet(process.env.PRIVATE_KEY);
const signature = await wallet.signMessage(orderHash);

// Example shown here if you're interacting with the exchange using an injected web3 provider such as metamask
const provider = new providers.Web3Provider(window.ethereum);
const signer = provider.getSigner();
const signature = await signer.signMessage(orderHash);

const signedOrder = { ...order, signature };

const result = await fetch("https://app.api.sportx.bet/orders/new", {
  method: "POST",
  body: JSON.stringify({ orders: [signedOrder] }),
  headers: { "Content-Type": "application/json" },
});
```

> The above command returns JSON structured like this

```json
{
  "status": "success",
  "data": {
    "orders": [
      "0x7a9d420551c4a635849013dd908f7894766e97aee25fe656d0c5ac857e166fac"
    ]
  }
}
```

This endpoint offers new orders on the exchange (market making)

### HTTP Request

`POST https://app.api.sportx.bet/orders/new`

### Request payload parameters

| Name   | Required | Type             | Description            |
| ------ | -------- | ---------------- | ---------------------- |
| orders | true     | SignedNewOrder[] | The new orders to post |

A `SignedNewOrder` object looks like this

| Name                     | Type    | Description                                                                                              |
| ------------------------ | ------- | -------------------------------------------------------------------------------------------------------- |
| marketHash               | string  | The market you wish to place this order under                                                            |
| maker                    | string  | The ethereum address offering the bet                                                                    |
| baseToken                | string  | The token this order is denominated in                                                                   |
| totalBetSize             | string  | The total bet size of the order in Ethereum units.                                                       |
| percentageOdds           | string  | The odds _the maker will be receiving_ as this order gets filled                                         |
| expiry                   | number  | Time in UNIX seconds after which this order is no longer valid                                           |
| executor                 | string  | The sportx.bet executor address. See the [metadata section](#get-metadata) for where to get this address |
| salt                     | string  | A random 32 byte string to differentiate between between orders with otherwise identical parameters      |
| isMakerBettingOutcomeOne | boolean | `true` if the maker is betting outcome one (and hence taker is betting outcome two if filled)            |
| signature                | string  | The signature of the maker on this order payload                                                         |

### Response format

| Name     | Type     | Description                                            |
| -------- | -------- | ------------------------------------------------------ |
| status   | string   | `success` or `failure` if the request succeeded or not |
| data     | object   | The response data                                      |
| > orders | string[] | The order hashes corresponding to the new orders       |

<!-- ## Cancel orders

```shell
curl --location --request POST 'https://app.api.sportx.bet/orders/cancel' \
--header 'Content-Type: application/json' \
--data-raw '{"message":"Are you sure you want to cancel these orders?","orders":["0x4ead6ef92741cd0b6e1ea32cb1d9586a85165e8bd780ab6f897992428c357bf1"],"cancelSignature":"0x1fe66a4ed7fbd2cf9e918f5b6b73db4f46166f871f7c0f293080ee07d63592ef0d29cd0aa37dc68e25a9d483515cc3ceb4934baaed8f0114385f8c43f28677aa1c"}'
```

```javascript
cosnt cancel
```

> The above command returns json structured like this

```json
{
  "status": "success",
  "data": {
    "orderHashes": [
      "0x4ead6ef92741cd0b6e1ea32cb1d9586a85165e8bd780ab6f897992428c357bf1"
    ]
  }
}
``` -->
