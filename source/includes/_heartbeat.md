# Heartbeat

Using the Heartbeat API, a user may register a `heartbeat`. An [API Key](#api-key) is necessary for this service. Once you register a heartbeat with the desired timeout value, all the user's open orders will be automatically cancelled if another heartbeat request is not sent within that timeout period.

This will ensure that when loss of connectivity occurs between the user and SX Bet API, they will have no exposure left on the orderbook.

## POST heartbeat

```shell
curl --location --request POST 'https://api.sx.bet/heartbeat' \
--header 'Content-Type: application/json' \
--header 'x-api-key: <YOUR-API-KEY>' \
--data-raw '{
    "requestor": "<YOUR-ACCOUNT-ADDRESS>",
    "timeoutSeconds": 10
}'
```

> The above command returns JSON structured like this

```json
{
    "status": "success",
    "data": {
        "requestor": "<YOUR-ACCOUNT-ADDRESS",
        "timeoutSeconds": 10,
        "expiresAt": "2024-11-12T14:35:06.614Z"
    }
}
```

### HTTP Request

`POST https://api.sx.bet/heartbeat`

### Request payload parameters

| Name           | Required | Type   | Description                                                                           |
| -------------- | -------- | ------ | ------------------------------------------------------------------------------------- |
| requestor      | true     | string | The ethereum address associated with your account                                     |
| timeoutSeconds | true     | number | The number of seconds before heartbeat service times out and cancels your open orders |

<aside class="notice">
The range `timeoutSeconds` can be is betwteen 0 - 3600 seconds inclusive. 
</aside>

### Response format

| Name             | Type   | Description                                                                           |
| ---------------- | ------ | ------------------------------------------------------------------------------------- |
| status           | string | `success` or `failure` if the request succeeded or not                                |
| data             | object | The response data                                                                     |
| > requestor      | string | The ethereum address associated with your account                                     |
| > timeoutSeconds | number | The number of seconds before heartbeat service times out and cancels your open orders |
| > expiresAt      | Date   | A JS Date object describing when the heartbeat will timeout/expire (UTC)              |
