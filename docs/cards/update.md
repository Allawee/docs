---
sidebar_position: 6
---

# Update a card

You can update your card’s controls and the card’s metadata. The update completely replaces the existing metadata, so you should include any data you wish to retain in the update object.

```js title="Sample Request"
curl https://api.allawee.com/cards/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "controls": {
    "allowedMcc": [
      "5541-5542,7654"
    ],
    "blockedMcc": [
      "7399",
      "7395"
    ],
    "allowedCategories": [
      "airlines"
    ],
    "blockedCategories": [
      "airlines"
    ],
    "allowedChannels": [
      "pos"
    ],
    "blockedChannels": [
      "online"
    ],
    "allowedMerchants": [
      "mch.2cbc123456"
    ],
    "blockedMerchants": [
      "mch.2cbc123456"
    ],
    "spendingLimits": [
      null
    ]
  },
  "metadata": {}
}'
-X PUT
```

| Request Body parameter | Required? | Description |
| :---- | :---- | :---- |
| controls | No | Controls for how and where the card can be used. |
| metadata | No | An object of information you wish to associate with the card. This field overwrites the existing metadata field when present, so you should include existing information you wish to retain. |

```js title="Sample Success Response"
{
    "code": "success",
    "data": {
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
    }
}
```
