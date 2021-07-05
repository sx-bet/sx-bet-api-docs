# Live scores

## Get live scores

```shell
curl --location --request POST 'https://app.api.sportx.bet/live-scores' \
--header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": [
    {
      "providerEventId": "7011313",
      "createdAt": "2021-05-27T18:56:45.128Z",
      "currentPeriod": "Full time",
      "extra": "[{\"Name\":\"Balls\",\"Value\":\"0\"},{\"Name\":\"Bases\",\"Value\":\"0/0/1\"},{\"Name\":\"Strikes\",\"Value\":\"0\"},{\"Name\":\"Outs\",\"Value\":\"3\"},{\"Name\":\"Turn\",\"Value\":\"1\"}]",
      "leagueId": 171,
      "periodTime": "-1",
      "periods": [
        {
          "label": "1st Inning",
          "isFinished": true,
          "teamOneScore": "0",
          "teamTwoScore": "1"
        },
        {
          "label": "2nd Inning",
          "isFinished": true,
          "teamOneScore": "0",
          "teamTwoScore": "0"
        },
        {
          "label": "3rd Inning",
          "isFinished": true,
          "teamOneScore": "0",
          "teamTwoScore": "0"
        },
        {
          "label": "4th Inning",
          "isFinished": true,
          "teamOneScore": "0",
          "teamTwoScore": "0"
        },
        {
          "label": "5th Inning",
          "isFinished": true,
          "teamOneScore": "0",
          "teamTwoScore": "0"
        },
        {
          "label": "6th Inning",
          "isFinished": true,
          "teamOneScore": "0",
          "teamTwoScore": "3"
        },
        {
          "label": "7th Inning",
          "isFinished": true,
          "teamOneScore": "1",
          "teamTwoScore": "0"
        },
        {
          "label": "Full time",
          "isFinished": true,
          "teamOneScore": "2",
          "teamTwoScore": "5"
        },
        {
          "label": "8th Inning",
          "isFinished": true,
          "teamOneScore": "0",
          "teamTwoScore": "0"
        },
        {
          "label": "9th Inning",
          "isFinished": true,
          "teamOneScore": "1",
          "teamTwoScore": "1"
        }
      ],
      "provider": "LSPORT",
      "sportId": 3,
      "teamOneScore": 2,
      "teamTwoScore": 5,
      "updatedAt": "2021-05-28T16:39:29.410Z",
      "sportXeventId": "L7011313"
    }
  ]
}
```

This endpoint retrieves live scores for a particular event ID.

### HTTP Request

`POST https://app.api.sportx.bet/live-scores`

### Request payload

| Name           | Required | Type     | Description           |
| -------------- | -------- | -------- | --------------------- |
| sportXEventIds | true     | string[] | An array of event IDs |

### Response format

| Name   | Type    | Description                                            |
| ------ | ------- | ------------------------------------------------------ |
| status | string  | `success` or `failure` if the request succeeded or not |
| data   | Score[] | The resulting scores for the fixtures passed in        |

A `Score` object has the following format

| Name          | Type     | Description                                                                     |
| ------------- | -------- | ------------------------------------------------------------------------------- |
| currentPeriod | string   | The current period label                                                        |
| extra         | string   | Extra data for this match                                                       |
| leagueId      | number   | The league ID for this match                                                    |
| periodTime    | number   | The time in the period. If it's -1, it is not available or the game is finished |
| periods       | Period[] | All of the periods in the match                                                 |

A `Period` object has the following format

| Name         | Type    | Description                          |
| ------------ | ------- | ------------------------------------ |
| label        | string  | The current period name              |
| isFinished   | boolean | `true` if the period is over         |
| teamOneScore | string  | The score of team one in this period |
| teamTwoScore | string  | The score of team two in this period |
