---
sidebar_position: 1
---

# Create a card

You can issue a card through the Allawee API with the create card endpoint. When you create a card, you can set controls on the cards. The categories determine when the card can be charged, through merchant categories, merchant MCCs, payment channels, and spending limits.

## Create a physical card

```js title="Sample Request"
curl https:api.allawee.comcards
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: applicationjson"
-d '{
  "program": "c.prg.2w2wBSRRjG6y1Ufuj",
  "amount": 500,
  "reference": "string",
  "cardHolderName": "string",
  "customer": "cus.2v4ryuthd4SWer",
  "debitSource": {},
  "fundingSource": {},
  "debitCurrency": "NGN",
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
| program | Yes | The ID for the card program you should have created, which the card being created will be placed under. |
| amount | Yes | The amount the card should be funded with on initial creation |
| fxHash | Yes | The fx hash for foreign currency transactions, which determines the exchange rate |
| reference | Yes | A unique reference for the card. |
| cardHolderName | No | The name of the person whom the card is being issued to. |
| customer | Yes | The ID of the customer whom the card is being issued to. |
| debitSource | No | The account to deduct from when creating the card. If this isn't passed and a debit currency is passed, it defaults to your main account with the chosen debit currency. |
| fundingSource | No | This determines where payment is pulled from while funding the card. |
| debitCurrency | No | The currency you wish to be charged in when creating a card. |
| controls | No | This field is an object that represents spending controls placed on the card. While the `controls` parameter is optional, once included, `allowedChannels`, `blockedChannels`, and `spendingLimits` have to be included in the controls object. |
| metadata | No | The metadata field can contain any values you want to associate with the card. |

```js title="Sample Success Response"
{
  "code": "success",
  "data": {
    "type": "virtual",
    "network": "mastercard",
    "status": "inactive",
    "currency": "USD",
    "customer": "cus.2tcqxRx4NoiGxnX65",
    "program": "c.prg.2u64yGpALXgHbqmjk",
    "metadata": {
      "name": "Hilda USD card"
    },
    "details": {
      "cardHolderName": "Bachi Hilda"
    },
    "createdAt": "2023-06-24T02:45:52.663Z",
    "updatedAt": "2023-06-24T02:45:52.663Z",
    "id": "c.2u6SXLG99Kq5a8TQ8",
    "object": "card"
  }
}
```

## Create a virtual card

You can create a naira virtual card like so:

```js title="Sample Request"
curl https:api.allawee.comcards
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: applicationjson"
-d '{
  "program": "c.prg.2w2wBSRRjG6y1Ufuj",
  "cardHolderName": "John Doe",
  "customer": "cus.2v4ryuthd4SWer",
  "debitSource": {},
  "fundingSource": {},
  "debitCurrency": "NGN",
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

You can create a virtual dollar card like so:

```js title="Sample Request"
curl https:api.allawee.comcards
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: applicationjson"
-d '{
  "program": "c.prg.2w2wBSRRjG6y1Ufuj",
  "cardHolderName": "John Doe",
  "customer": "cus.2v4ryuthd4SWer",
  "fxHash": "a6454tgrfdcvhhyue64645ref45363jh",
  "debitCurrency": "NGN",
  "amount": 1000,
  "debitSource": {},
  "fundingSource": {},
  "debitCurrency": "NGN",
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