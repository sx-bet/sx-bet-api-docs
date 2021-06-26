# Leagues

## Get leagues

```shell
curl --location --request GET 'https://app.api.sportx.bet/leagues'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": [
    {
      "leagueId": 20,
      "label": "The Memorial Tournament_Round 1",
      "sportId": 4,
      "active": false,
      "homeTeamFirst": true
    },
    {
      "leagueId": 5,
      "label": "The Masters_Round 1",
      "sportId": 4,
      "active": false,
      "homeTeamFirst": true
    },
    {
      "leagueId": 1,
      "label": "NBA",
      "sportId": 1,
      "active": true,
      "homeTeamFirst": false
    },
    {
      "leagueId": 28,
      "label": "US Open_Round 4",
      "sportId": 4,
      "active": false,
      "homeTeamFirst": true
    },
    {
      "leagueId": 10,
      "label": "Wells Fargo Championship_Round 1",
      "sportId": 4,
      "active": false,
      "homeTeamFirst": true
    },
    {
      "leagueId": 37,
      "label": "RBC Heritage_Round 4",
      "sportId": 4,
      "active": false,
      "homeTeamFirst": true
    },
    {
      "leagueId": 3,
      "label": "NHL",
      "sportId": 2,
      "active": true,
      "homeTeamFirst": false
    },
    {
      "leagueId": 34,
      "label": "UFC",
      "sportId": 7,
      "active": true,
      "homeTeamFirst": true
    }
  ]
}
```

This endpoint returns all the leagues supported by SportX

### HTTP Request

`GET https://app.api.sportx.bet/leagues`

### Response format

| Name   | Type     | Description                                            |
| ------ | -------- | ------------------------------------------------------ |
| status | string   | `success` or `failure` if the request succeeded or not |
| data   | League[] | An array of league objects                             |

A `League` object looks like this

| Name          | Type    | Description                                                                                                                                                              |
| ------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| leagueID      | number  | The ID for this league                                                                                                                                                   |
| label         | string  | The name of this league                                                                                                                                                  |
| sportID       | number  | The ID of the sport this league corresponds to                                                                                                                           |
| active        | boolean | Whether or not the league is active on SportX currently                                                                                                                  |
| homeTeamFirst | boolean | Instructions to the client of how to show the team names for markets in this league. `true` if the home team is `teamOneName`, `false` if the home team is `teamTwoName` |

## Get active leagues

```shell
curl --location --request GET 'https://app.api.sportx.bet/leagues/active'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": [
    {
      "leagueId": 34,
      "label": "UFC",
      "sportId": 7,
      "homeTeamFirst": true,
      "numberOfEvents": 40
    },
    {
      "leagueId": 10065,
      "label": "Bitcoin",
      "sportId": 14,
      "homeTeamFirst": true,
      "numberOfEvents": 15
    },
    {
      "leagueId": 10064,
      "label": "Ethereum",
      "sportId": 14,
      "homeTeamFirst": true,
      "numberOfEvents": 19
    },
    {
      "leagueId": 171,
      "label": "MLB",
      "sportId": 3,
      "homeTeamFirst": false,
      "numberOfEvents": 14
    },
    {
      "leagueId": 1,
      "label": "NBA",
      "sportId": 1,
      "homeTeamFirst": false,
      "numberOfEvents": 6
    },
    {
      "leagueId": 1290,
      "label": " Azerbaijan GP",
      "sportId": 12,
      "homeTeamFirst": false,
      "numberOfEvents": 1
    },
    {
      "leagueId": 1265,
      "label": "WNBA",
      "sportId": 1,
      "homeTeamFirst": false,
      "numberOfEvents": 4
    }
  ]
}
```

This endpoint returns all the currently active leagues with markets in them

### HTTP Request

`GET https://app.api.sportx.bet/leagues/active`

### Response format

See [get leagues section](#get-leagues) for how the `League` object is formatted
