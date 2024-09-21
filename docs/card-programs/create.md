---
sidebar_position: 2
---

# Creating a card program

## Creating a Physical Card programme

Cards you subsequently create will be within a card program. You need to create a card program before you can create physical cards, as you have to assign the physical card to a program at the point of creation.

```js title="Sample Request"
curl https://api.allawee.com/card-programs
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "name": "string",
  "description": "string",
  "network": "verve",
  "type": "physical",
  "quantity": 1,
  "currency": "NGN",
  "distribution": {
    "type": "bulked",
    "shippingAddress": {
      "city": "Yaba",
      "state": "Lagos",
      "countryCode": "NG",
      "phoneNumber": "+2348123456789",
      "addressLineOne": "No 10, Adekunle Close",
      "addressLineTwo": "Off Ciroma Rd"
    },
    "returnAddress": {
      "city": "Yaba",
      "state": "Lagos",
      "countryCode": "NG",
      "phoneNumber": "+2348123456789",
      "addressLineOne": "No 10, Adekunle Close",
      "addressLineTwo": "Off Ciroma Rd"
    }
  },
  "personalization": {
    "frontArtworkFile": "string",
    "printCardholderName": true,
    "defaultCardholderName": "string"
  },
  "authorization": {
    "fundingSourceType": "settlement-account",
    "settlementAccount": {},
    "transactionFee": {},
    "webhook": {},
    "timeoutDefault": "decline"
  }
}'
-X POST
```

| Request Body parameter | Required? | Description |
| :---- | :---- | :---- |
| name | Yes | A unique name identifier for your card program. It should be a string. |
| description | No | A string description for your card program. |
| network | Yes | The card network for cards within the program. Allawee currently supports issuing `verve` and `mastercard` cards. |
| type | Yes | This parameter specifies whether the cards within the program should be `virtual` or `physical` cards. |
| quantity | No | The number of cards that will be within the card program. This is required for creating physical cards. |
| currency | Yes | The currency for the cards within the program. Allawee currently supports issuing `NGN` and `USD` cards. |
| distribution | No | This should be present for physical cards and determines the delivery and return addresses for cards within the program. It is an object that should have a `type`, `shippingAddress`, and `returnAddress`. The type may be `individually`, for cards that should be delivered to separate addresses, and `bulked`, for cards that should be delivered together. |
| personalization | No | This should be present for physical cards. It determines the artwork on the card and whether the card holder’s name should be on the card. |
| authorization | No | This should be present for physical cards. The authorization parameter determines important information such as the card’s funding source, which may be `card-account` or `settlement-account`. It also determines the authorization timeout default action which may be `approve` or `decline`. |

```js title="Sample Success Response"
{
    "code": "success",
    "data": {
        "name": "Card program",
        "network": "verve",
        "quantity": 1,
        "currency": "NGN",
        "personalization": {
            "frontArtworkFile": "https://figma.com",
            "printCardholderName": false,
            "defaultCardholderName": "Ciroma"
        },
        "distribution": {
            "type": "bulked",
            "shippingAddress": {
                "city": "yaba",
                "state": "NG-LA",
                "countryCode": "NG",
                "phoneNumber": "+2349134902345",
                "addressLineOne": "100 Herbert macaulay way",
                "addressLineTwo": ""
            }
        },
        "authorization": {
            "fundingSourceType": "settlement-account",
            "webhook": "wh.2tXPfsNc6CoZjbRWi",
            "settlementAccount": "acct.2tVZczWw7m6Teoeb7",
            "feesAccount": "acct.2tVZczWw7m6Teoeb7",
            "timeoutDefault": "decline"
        },
        "status": "new",
        "createdAt": "2023-03-17T00:39:22.589Z",
        "updatedAt": "2023-03-17T00:39:22.589Z",
        "id": "c.prg.2tY3gamDwgZfxnKHS",
        "object": "card.program"
    }
}
```

## Creating a Virtual Card programme

Virtual card programmes are live immediately they are created.

```js title="Sample Request"
curl https://api.allawee.com/card-programs
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "name": "string",
  "network": "mastercard",
  "type": "virtual",
  "currency": "NGN",
  "authorization": {
    "fundingSourceType": "settlement-account",
    "settlementAccount": {},
    "transactionFee": {},
    "webhook": {},
    "timeoutDefault": "decline"
  }
}'
-X POST
```

| Request Body parameter | Required? | Description |
| :---- | :---- | :---- |
| name | Yes | A unique name identifier for your card program. It should be a string. |
| network | Yes | The card network for cards within the program. Allawee currently supports issuing `verve` and `mastercard` cards. |
| type | Yes | This parameter specifies whether the cards within the program should be `virtual` or `physical` cards. |
| currency | Yes | The currency for the cards within the program. Allawee currently supports issuing `NGN` and `USD` cards. |
| authorization | No | This should be present for physical cards. The authorization parameter determines important information such as the card’s funding source, which may be `card-account` or `settlement-account`. It also determines the authorization timeout default action which may be `approve` or `decline`. |

```js title="Sample Success Response"
{
    "code": "success",
    "data": {
        "name": "Card program",
        "network": "mastercard",
        "currency": "NGN",
        "authorization": {
            "fundingSourceType": "settlement-account",
            "webhook": "wh.2tXPfsNc6CoZjbRWi",
            "settlementAccount": "acct.2tVZczWw7m6Teoeb7",
            "feesAccount": "acct.2tVZczWw7m6Teoeb7",
            "timeoutDefault": "decline"
        },
        "status": "new",
        "createdAt": "2023-03-17T00:39:22.589Z",
        "updatedAt": "2023-03-17T00:39:22.589Z",
        "id": "c.prg.2tY3gamDwgZfxnKHS",
        "object": "card.program"
    }
}
```