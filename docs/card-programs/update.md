---
sidebar_position: 4
---

# Update a card program

You can update card programs you have already created. The request body is similar to the request body for creating a new card program. However, it should be a `PUT` request to https://api.allawee.com/card-programs/:id like so:

```
curl https://api.allawee.com/card-programs/:id
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
-X PUT
```

You cannot update a card program once it has been approved.
