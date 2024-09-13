---
sidebar_position: 7
---

# Fetch cards and card secrets

You can get all your cards or get a particular card by the ID.

To get all of your cards:

```js title="Sample Request"
curl https://api.allawee.com/cards
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": [
        {
            "type": "physical",
            "status": "active",
            "currency": "NGN",
            "program": "cp.2tXPDcLLvvXGeTNk9",
            "details": {
                "last4": "4880",
                "expiry": "03/26",
                "cardHolderName": "Ciroma C Adekunle"
            },
            "createdAt": "2023-03-14T23:58:35.879Z",
            "updatedAt": "2023-03-15T00:11:43.844Z",
            "controls": {
                "allowedCategories": [
                    "flight-ticket"
                ],
                "blockedCategories": [
                    "betting"
                ],
                "spendingLimits": [
                    {
                        "amount": 1000,
                        "interval": "monthly"
                    }
                ]
            },
            "customer": "cus.2tXNjMhytgx7hCxu9",
            "metadata": {
                "name": "Ciroma's travel card"
            },
            "id": "c.2tXPDv41Ri2qewJXL",
            "object": "card"
        },
        {
            "type": "physical",
            "status": "active",
            "currency": "NGN",
            "program": "cp.2tVgh75y8WhKw6Eke",
            "details": {
                "last4": "2668",
                "expiry": "03/26",
                "cardHolderName": "Damini"
            },
            "createdAt": "2023-03-09T19:16:42.419Z",
            "updatedAt": "2023-03-10T22:03:39.928Z",
            "controls": {
                "allowedCategories": [
                    "betting",
                    "flight-ticket",
                    "hospitality"
                ],
                "allowedChannels": [
                    "atm",
                    "pos",
                    "online"
                ],
                "spendingLimits": [
                    {
                        "amount": 400000000,
                        "interval": "monthly"
                    }
                ]
            },
            "customer": "cus.2tVZh8GkvSJu6xgRJ",
            "metadata": {
                "userId": "1234"
            },
            "id": "c.2tVghquVL5LxCkjB3",
            "object": "card"
        },
        {
            "type": "physical",
            "status": "inactive",
            "currency": "NGN",
            "program": "cp.2tVZiNd3wyUUPRiSR",
            "details": {
                "last4": "3681",
                "expiry": "03/26",
                "cardHolderName": "Iyabu"
            },
            "createdAt": "2023-03-09T11:13:33.144Z",
            "updatedAt": "2023-03-09T16:59:29.928Z",
            "controls": {
                "blockedCategories": [
                    "betting",
                    "flight-ticket",
                    "hospitality"
                ],
                "blockedChannels": [
                    "atm",
                    "pos",
                    "online"
                ],
                "spendingLimits": [
                    {
                        "amount": 300000000,
                        "interval": "monthly"
                    }
                ]
            },
            "customer": "cus.2tVZh8GkvSJu6xgRJ",
            "metadata": {
                "userId": "1234"
            },
            "id": "c.2tVaLqrmte2zCuPbM",
            "object": "card"
        }
    ],
    "metadata": {
        "hasMore": false
    }
}
```

To get a single card by the card ID:

```js title="Sample Request"
curl https://api.allawee.com/cards/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": {
        "type": "physical",
        "status": "active",
        "currency": "NGN",
        "program": "cp.2tVgh75y8WhKw6Eke",
        "details": {
            "last4": "2668",
            "expiry": "03/26",
            "cardHolderName": "Damini"
        },
        "createdAt": "2023-03-09T19:16:42.419Z",
        "updatedAt": "2023-03-10T22:03:39.928Z",
        "controls": {
            "allowedCategories": [
                "betting",
                "flight-ticket",
                "hospitality"
            ],
            "allowedChannels": [
                "atm",
                "pos",
                "online"
            ],
            "spendingLimits": [
                {
                    "amount": 400000000,
                    "interval": "monthly"
                }
            ]
        },
        "customer": "cus.2tVZh8GkvSJu6xgRJ",
        "metadata": {
            "userId": "1234"
        },
        "id": "c.2tVghquVL5LxCkjB3",
        "object": "card"
    }
}
```

You can also get a card’s secrets:

```js title="Sample Request"
curl https://api.allawee.com/cards/:id/secrets
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": {
        "cardHolderName": "Ciroma C Adekunle",
        "last4": "4880",
        "pan": "5061462473446064880",
        "expiry": "03/26",
        "cvv": "123"
    }
}
```
