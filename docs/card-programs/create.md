---
sidebar_position: 2
---

# Creating a card program

Cards you subsequently create will be within a card program. You need to create a card program before you can create physical cards, as you have to assign the physical card to a program at the point of creation.

```
curl https://api.allawee.com/card-programs
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "name": "string",
  "description": "string",
  "network": "verve",
  "type": "virtual",
  "quantity": 0,
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

