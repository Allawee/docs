---
sidebar_position: 6
---

# Update a card

You can update your card’s controls and the card’s metadata. The update completely replaces the existing metadata, so you should include any data you wish to retain in the update object.

```
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
