---
sidebar_position: 4
---

# Link a card

You can link a card you’ve created to your customer through either the card’s ID or the card PAN.

To link a card to a customer through the card’s ID, you should include the ID in the url.

```
curl https://api.allawee.com/cards/:id/link
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "reference": "string",
  "cardHolderName": "string",
  "customer": "string",
  "fundingSource": {},
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
-X POST
```

| Request Body parameter | Required? | Description |
| :---- | :---- | :---- |
| reference | No | A unique reference. |
| cardHolderName | No | The name of the card holder. |
| customer | Yes | The ID of the customer you wish to link to the card. |
| fundingSource | No | The hash for the conversion. This is only necessary when the debit source and the card have different currencies. |
| controls | No | While controls isn’t a required field, if present, it should include `allowedChannels`, `blockedChannels`, and `spendingLimits`. |
| metadata | No | This is an object you can use to attach any data of your choice to the card link. |

You can also link your cards to your customers through the card PAN.

```
curl https://api.allawee.com/cards/:id/link
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "reference": "string",
  "pan": "string",
  "cardHolderName": "string",
  "customer": "string",
  "fundingSource": {},
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
  "depositChannels": [
    "bank-account"
  ],
  "metadata": {}
}'
-X POST
```

The request schema is similar to linking a card by ID, with the addition of two values.

| Request Body parameter | Required? | Description |
| :---- | :---- | :---- |
| pan | Yes | The PAN for the card you want to link to the customer. |
