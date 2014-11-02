# Dogetipbot API v1

## Overview

Version 1 of the dogetipbot API allows you to query your account balance and history. More endpoints will be rolled out in later API versions.

### API Version

The current stable API version is **v1**. To ensure compatibility, future API versions will include an updated endpoint URL version number.

#### Example Requests

### Formats

The base URL for all API resources is `https://dogetipbot.com/api/v1/`.

All data is sent and received as [JSON][]. Blank fields are included as `null` instead of being omitted.

[JSON]: http://www.json.org/

### Errors

All error responses are in the following format, delivered with the corresponding status code:

```json
{
    "message":"Invalid API Key",
    "status":401,
    "error":"Unauthorized"
}
```

The response status code will always be `200` to allow browsers to parse it. Check the body of the response for the actual error data.

## Rate Limits & Caching

The API request limit is 20 requests/min. Requests beyond this limit will return an error message with a status code of 429 (Too Many Requests).

History responses are cached for one minute.

## Authentication 

All API endpoints require an API key to be passed in the request header. API keys are generated in the API section of the dogetipbot dashboard (https://dogetipbot.com/dashboard/api).

````bash
curl -H "Authorization: API-KEY <xxxxxxxxxx-xxxxxxxxxx>" https://dogetipbot.com/api/v1/
````

## Endpoints

### Balance (GET)

Return the current account balance.

````bash
curl -H "Authorization: API-KEY <xxxxxxxxxx-xxxxxxxxxx>" https://dogetipbot.com/api/v1/balance.json
````

````json
{
    "address": "DHxFH9wekP93esJ...",
    "balance": "1550.00000000"
}
````

### History (GET)

Return the last 50 transactions for the account.

````bash
curl -H "Authorization: API-KEY <xxxxxxxxxx-xxxxxxxxxx>" https://dogetipbot.com/api/v1/history.json
````

````json
{
    "address": "DHxFH9wekP93esJ...",
    "transactions": [{
        "service": "reddit",
        "type": "withdraw",
        "state": "completed",
        "from_user": "user1",
        "to_user": null,
        "to_address": "DHxFH9wekP93esJ...",
        "amount": "60.00000000",
        "fiat": "$0.0086244000 USD",
        "timestamp": "2014-08-28 03:13:17"
    }, {
        "service": "reddit",
        "type": "tip",
        "state": "completed",
        "from_user": "user1",
        "to_user": "user2",
        "to_address": null,
        "amount": "6.00000000",
        "fiat": "$0.0008586600 USD",
        "timestamp": "2014-08-27 23:43:19"
    }]
}
````