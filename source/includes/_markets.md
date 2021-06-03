# Markets

## Get active markets

```shell
curl --location --request GET 'https://stage.api.sportx.bet/markets/active?onlyMainLine=true'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "markets": [
      {
        "status": "ACTIVE",
        "marketHash": "0x0d64c52e8781acdada86920a2d1e5acd6f29dcfe285cf9cae367b671dff05f7d",
        "outcomeOneName": "Nikoloz Basilashvili",
        "outcomeTwoName": "Carlos Alcaraz",
        "outcomeVoidName": "NO_CONTEST",
        "teamOneName": "Nikoloz Basilashvili",
        "teamTwoName": "Carlos Alcaraz",
        "type": "MONEY_LINE",
        "gameTime": 1622735700,
        "sportXeventId": "L7032829",
        "liveEnabled": true,
        "sportLabel": "Tennis",
        "sportId": 6,
        "leagueId": 1070,
        "homeTeamFirst": true,
        "leagueLabel": "ATP French Open",
        "group1": "ATP French Open"
      },
      {
        "status": "ACTIVE",
        "marketHash": "0xe609a49d083cd41214a0db276c1ba323c4a947eefd2e4260386fec7b5d258188",
        "outcomeOneName": "Over 36.5",
        "outcomeTwoName": "Under 36.5",
        "outcomeVoidName": "NO_GAME_OR_EVEN",
        "teamOneName": "Nikoloz Basilashvili",
        "teamTwoName": "Carlos Alcaraz",
        "type": "OVER_UNDER",
        "gameTime": 1622735700,
        "line": 36.5,
        "sportXeventId": "L7032829",
        "liveEnabled": true,
        "sportLabel": "Tennis",
        "sportId": 6,
        "leagueId": 1070,
        "homeTeamFirst": true,
        "leagueLabel": "ATP French Open",
        "mainLine": true,
        "group1": "ATP French Open"
      },
      {
        "status": "ACTIVE",
        "marketHash": "0x85e588d72b4a2ec6386846a6f4706dba2124410e38bd8e8f7f37dee9728e0d84",
        "outcomeOneName": "Nikoloz Basilashvili +1.5",
        "outcomeTwoName": "Carlos Alcaraz -1.5",
        "outcomeVoidName": "NO_GAME_OR_EVEN",
        "teamOneName": "Nikoloz Basilashvili",
        "teamTwoName": "Carlos Alcaraz",
        "type": "SPREAD",
        "gameTime": 1622735700,
        "line": 1.5,
        "sportXeventId": "L7032829",
        "liveEnabled": true,
        "sportLabel": "Tennis",
        "sportId": 6,
        "leagueId": 1070,
        "homeTeamFirst": true,
        "leagueLabel": "ATP French Open",
        "mainLine": true,
        "group1": "ATP French Open"
      }
    ]
  }
}
```

This endpoint retrieves active markets on the exchange

### HTTP Request

`GET https://stage.api.sportx.bet/markets/active`

### Query parameters

| Name         | Required | Type      | Description                                                                              |
| ------------ | -------- | --------- | ---------------------------------------------------------------------------------------- |
| onlyMainLine | false    | false     | If set to true, the result will only include main lines on spread and over under markets |
| eventId      | false    | undefined | If set, it will only include markets for a particular sportXeventId                      |
| leagueID     | false    | undefined | If set, it will only include markets for a particular league ID                          |
| liveOnly     | false    | false     | If set, it will only include markets that are currently available for in-play betting    |
| betGroup     | false    | undefined | If set, it will only include markets for a particular bet group                          |

### Response format

| Name      | Type     | Description                  |
| --------- | -------- | ---------------------------- |
| status    | string   | `success` or `failure` if the request succeeded or not |
| data      | object   | The response data            |
| > markets | Market[] | The active markets           |

A `market` object looks like this

| Name            | Type       | Description                                                                         |
| --------------- | ---------- | ----------------------------------------------------------------------------------- |
| status          | string     | `ACTIVE` or `INACTIVE`                                                              |
| marketHash      | string     | The unique identifier for the market                                                |
| outcomeOneName  | string     | Outcome one for this market                                                         |
| outcomeTwoName  | string     | Outcome two for this market                                                         |
| outcomeVoidName | string     | Outcome void for this market                                                        |
| teamOneName     | string     | The name of the first team/player participating                                     |
| teamTwoName     | string     | The name of the second team/player participating                                    |
| type            | MarketType | The type of the market                                                              |
| gameTime        | number     | The UNIX timestamp of the game                                                      |
| line            | number?    | The line of the market (only applicable to markets with a line, for example SPREAD) |
| sportXeventId   | string     | The unique event ID for this market                                                 |
| liveEnabled     | boolean    | Whether or not this match is available for live betting                             |
| sportLabel      | string     | The name of the sport for this market                                               |
| leagueID        | number     | The league ID for this market                                                       |
| homeTeamFirst   | boolean    | Indicator to the client of whether to display the home team first or not            |
| leagueLabel     | string     | The name of the league for this market                                              |
| mainLine        | boolean   | If this market is currently the main line or not                                    |
| group1          | string     | Indicator to the client of how to display this market                               |
| group2          | string?    | Indicator to the client of how to display this market                               |

A `MarketType` can currently be one of the following

- `OVER_UNDER`
- `SPREAD`
- `MONEY_LINE`
- `OUTRIGHT_WINNER`

## Get specific markets

```shell
curl --location --request POST 'https://stage.api.sportx.bet/markets/find' \
--header 'Content-Type: application/json' \
--data-raw '{
    "marketHashes": ["0x3cba25f2253035b015b9bb555c1bf900f6737704d57425dd2a5b60e929c33b81"]
}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": [
    {
      "status": "ACTIVE",
      "marketHash": "0x3cba25f2253035b015b9bb555c1bf900f6737704d57425dd2a5b60e929c33b81",
      "outcomeOneName": "Over 2.5",
      "outcomeTwoName": "Under 2.5",
      "outcomeVoidName": "NO_GAME_OR_EVEN",
      "teamOneName": "Aston Villa",
      "teamTwoName": "Burnley",
      "type": "OVER_UNDER",
      "gameTime": 1608228000,
      "line": 2.5,
      "reportedDate": 1608234719,
      "outcome": 2,
      "teamOneScore": 0,
      "teamTwoScore": 0,
      "sportXeventId": "L6247212",
      "liveEnabled": false,
      "sportLabel": "Soccer",
      "sportId": 5,
      "leagueId": 29,
      "homeTeamFirst": true,
      "leagueLabel": "English Premier League",
      "group1": "English Premier League"
    }
  ]
}
```

This endpoint retrieves specific markets

### HTTP Request

`POST https://stage.api.sportx.bet/markets/find`

### Request format

| Name         | Required | Type     | Description                                  |
| ------------ | ---- | -------- | -------------------------------------------- |
| marketHashes | true | string[] | The market hashes of the markets to retrieve |

### Response format

| Name   | Type     | Description                  |
| ------ | -------- | ---------------------------- |
| status | string   | `success` or `failure` if the request succeeded or not |
| data   | Market[] | The response data            |

See [active markets section](#get-active-markets) for how the `Market` object is formatted

## Popular markets

```shell
curl --location --request GET 'https://stage.api.sportx.bet/markets/popular'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": [
    {
      "status": "ACTIVE",
      "marketHash": "0x66fc26c008c724d5dec2fb0bf8fb8797ecc49a4302a785cc8e5e7faf96249d8a",
      "outcomeOneName": "Ismagulov D.",
      "outcomeTwoName": "Rafael da Silva Alves",
      "outcomeVoidName": "NO_GAME",
      "teamOneName": "Ismagulov D.",
      "teamTwoName": "Rafael da Silva Alves",
      "type": "MONEY_LINE",
      "gameTime": 1621724400,
      "sportXeventId": "L6896568",
      "liveEnabled": false,
      "sportLabel": "Mixed Martial Arts",
      "sportId": 7,
      "leagueId": 34,
      "homeTeamFirst": true,
      "leagueLabel": "UFC",
      "group1": "UFC"
    },
    {
      "status": "ACTIVE",
      "marketHash": "0xad3494f1bf10e826cd8e0faecd42e0f578f2bc9de748946fbe3d833a11764b89",
      "outcomeOneName": "West Ham United -0.5",
      "outcomeTwoName": "Southampton +0.5",
      "outcomeVoidName": "NO_GAME_OR_EVEN",
      "teamOneName": "West Ham United",
      "teamTwoName": "Southampton",
      "type": "SPREAD",
      "gameTime": 1621782000,
      "line": -0.5,
      "sportXeventId": "L6973172",
      "liveEnabled": false,
      "sportLabel": "Soccer",
      "sportId": 5,
      "leagueId": 29,
      "homeTeamFirst": true,
      "leagueLabel": "English Premier League",
      "mainLine": true,
      "group1": "English Premier League"
    }
  ]
}
```

This endpoint retrieves the top 10 popular markets by volume.

### HTTP Request

`GET https://stage.api.sportx.bet/markets/popular`

### Response format

| Name   | Type     | Description                  |
| ------ | -------- | ---------------------------- |
| status | string   | `success` or `failure` if the request succeeded or not |
| data   | Market[] | The response data            |

See [active markets section](#get-active-markets) for how the `Market` object is formatted
