---
sidebar_position: 1
---

# Card Transactions

You can fetch a list of all card transactions through the card transactions endpoint. This endpoint shows you a list of transactions that have occurred on cards you have issued.

```js title="Sample Request"
curl https://api.allawee.com/card-transactions
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": [
        {
            "updatedAt": "2024-09-04T23:36:48.428Z",
            "type": "capture",
            "authorization": "c.auth.2xxxxxxx",
            "currency": "NGN",
            "createdAt": "2024-09-04T23:36:48.428Z",
            "channel": "pos",
            "mcc": "5541",
            "card": "c.2xxxxxxx",
            "source": "c.auth.2xxxxxxx",
            "customer": "cus.2xxxxxxx",
            "amount": 5200000,
            "fees": 0,
            "networkData": {
                "stan": "378385",
                "rrn": "172549337719",
                "reference": "8375254037",
                "terminalId": "201168PJ",
                "cardAcceptorNameLocation": "LARONDE NIGERIA LIMITED140 MURITALA XXNG",
                "network": "verve"
            },
            "id": "c.txn.2xxxxxxx",
            "object": "card.transaction"
        }
    ],
    "metadata": {
        "hasMore": false
    }
}
}
```

You can also fetch a single card transaction by the ID.

```js title="Sample Request"
curl https://api.allawee.com/card-transactions/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": {
        "updatedAt": "2024-09-04T23:36:48.428Z",
        "type": "capture",
        "authorization": "c.auth.2xxxxxxx",
        "currency": "NGN",
        "createdAt": "2024-09-04T23:36:48.428Z",
        "channel": "pos",
        "mcc": "5541",
        "card": "c.2xxxxxxx",
        "source": "c.auth.2xxxxxxx",
        "customer": "cus.2xxxxxxx",
        "amount": 5200000,
        "fees": 0,
        "networkData": {
            "stan": "378385",
            "rrn": "172549337719",
            "reference": "8375254037",
            "terminalId": "201168PJ",
            "cardAcceptorNameLocation": "LARONDE NIGERIA LIMITED140 MURITALA XXNG",
            "network": "verve"
        },
        "id": "c.txn.2xxxxxxx",
        "object": "card.transaction"
    }
}
```
