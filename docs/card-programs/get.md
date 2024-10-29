---
sidebar_position: 3
---

# Getting Card Programs

You can get all your card programs or get a particular card program by the ID.

To get all of your card programs:

```js title="Sample Request"
curl https://api.allawee.com/card-programs
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

To get a single card program by the program ID:

```js title="Sample Request"
curl https://api.allawee.com/card-programs/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": [
        {
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
        },
        {
            "name": "Baggy",
            "network": "verve",
            "quantity": 1,
            "currency": "NGN",
            "personalization": {
                "frontArtworkFile": "https://figma.com",
                "printCardholderName": false,
                "defaultCardholderName": "Ciroma C Adekunle"
            },
            "distribution": {
                "type": "bulked",
                "shippingAddress": {
                    "city": "mainland",
                    "state": "NG-LA",
                    "countryCode": "NG",
                    "phoneNumber": "+2349154109322",
                    "addressLineOne": "100 herbert macaulay raod",
                    "addressLineTwo": null
                }
            },
            "authorization": {
                "fundingSourceType": "settlement-account",
                "webhook": "wh.2tXPCopj8N4QFSZsM",
                "settlementAccount": "acct.2tVZczWw7m6Teoeb7",
                "feesAccount": "acct.2tVZczWw7m6Teoeb7",
                "timeoutDefault": "decline"
            },
            "status": "live",
            "createdAt": "2023-03-14T23:58:11.236Z",
            "updatedAt": "2023-03-14T23:58:35.902Z",
            "id": "c.prg.2tXPDcLLvvXGeTNk9",
            "object": "card.program"
        },
        {
            "name": "Chattered",
            "network": "verve",
            "quantity": 1,
            "currency": "NGN",
            "personalization": {
                "frontArtworkFile": "https://figma.com",
                "printCardholderName": false,
                "defaultCardholderName": "Damini"
            },
            "distribution": {
                "type": "bulked",
                "shippingAddress": {
                    "city": "Mainland",
                    "state": "NG-LA",
                    "countryCode": "NG",
                    "phoneNumber": "+2349154109256",
                    "addressLineOne": "44 commercial avenue",
                    "addressLineTwo": null
                }
            },
            "authorization": {
                "fundingSourceType": "settlement-account",
                "webhook": "wh.2tVZfLBEWKwRvt7Lf",
                "settlementAccount": "acct.2tVZczWw7m6Teoeb7",
                "feesAccount": "acct.2tVZczWw7m6Teoeb7",
                "timeoutDefault": "decline"
            },
            "status": "live",
            "createdAt": "2023-03-09T19:15:44.757Z",
            "updatedAt": "2023-03-09T19:16:42.443Z",
            "id": "c.prg.2tVgh75y8WhKw6Eke",
            "object": "card.program"
        },
        {
            "name": "Opay",
            "network": "verve",
            "quantity": 1,
            "currency": "NGN",
            "personalization": {
                "frontArtworkFile": "https://figma.com",
                "printCardholderName": false,
                "defaultCardholderName": "Iyabu"
            },
            "distribution": {
                "type": "bulked",
                "shippingAddress": {
                    "city": "mainland",
                    "state": "NG-LA",
                    "countryCode": "NG",
                    "phoneNumber": "+2349154109238",
                    "addressLineOne": "44 commerical road",
                    "addressLineTwo": null
                }
            },
            "authorization": {
                "fundingSourceType": "settlement-account",
                "webhook": "wh.2tVZfLBEWKwRvt7Lf",
                "settlementAccount": "acct.2tVZczWw7m6Teoeb7",
                "feesAccount": "acct.2tVZczWw7m6Teoeb7",
                "timeoutDefault": "decline"
            },
            "status": "live",
            "createdAt": "2023-03-09T10:25:48.738Z",
            "updatedAt": "2023-03-09T11:13:33.205Z",
            "id": "c.prg.2tVZiNd3wyUUPRiSR",
            "object": "card.program"
        }
    ],
    "metadata": {
        "hasMore": false
    }
}
```