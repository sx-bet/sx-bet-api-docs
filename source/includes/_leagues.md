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

### Query parameters

| Name    | Required | Type   | Description                                       |
| ------- | -------- | ------ | ------------------------------------------------- |
| sportId | false    | number | Only return leagues for this particular sport ID. |

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
      "eventsByType": {
        "game-lines": 36
      }
    },
    {
      "leagueId": 30,
      "label": "Champions League_UEFA",
      "sportId": 5,
      "homeTeamFirst": true,
      "eventsByType": {
        "outright-winner": 32,
        "game-lines": 10
      }
    },
    {
      "leagueId": 29,
      "label": "English Premier League",
      "sportId": 5,
      "homeTeamFirst": true,
      "eventsByType": {
        "outright-winner": 23,
        "game-lines": 10
      }
    },
    {
      "leagueId": 1197,
      "label": "UEFA Nations League",
      "sportId": 5,
      "homeTeamFirst": true,
      "eventsByType": {
        "outright-winner": 19,
        "game-lines": 2
      }
    },
    {
      "leagueId": 244,
      "label": "Bundesliga",
      "sportId": 5,
      "homeTeamFirst": true,
      "eventsByType": {
        "game-lines": 9,
        "outright-winner": 18
      }
    },
    {
      "leagueId": 1114,
      "label": "La Liga",
      "sportId": 5,
      "homeTeamFirst": true,
      "eventsByType": {
        "game-lines": 10,
        "outright-winner": 37
      }
    },
    {
      "leagueId": 1112,
      "label": "Ligue 1",
      "sportId": 5,
      "homeTeamFirst": true,
      "eventsByType": {
        "game-lines": 20,
        "outright-winner": 20
      }
    },
    {
      "leagueId": 1113,
      "label": "Serie A",
      "sportId": 5,
      "homeTeamFirst": true,
      "eventsByType": {
        "outright-winner": 20,
        "game-lines": 10
      }
    },
    {
      "leagueId": 1236,
      "label": "Portugal Primeira Liga",
      "sportId": 5,
      "homeTeamFirst": true,
      "eventsByType": {
        "outright-winner": 17,
        "game-lines": 9
      }
    }
  ]
}
```

This endpoint returns all the currently active leagues with markets in them.

<aside class="notice">
Note that this endpoint is only updated every 10m.
</aside>

### HTTP Request

`GET https://app.api.sportx.bet/leagues/active`

### Response format

See [get leagues section](#get-leagues) for how the response object is formatted. There is an additional field `eventsByType` which maps the number of unique events within a particular bet group (for example, `game-lines` or `outright-winner`).
