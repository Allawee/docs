---
sidebar_position: 1
---

# Card Transactions

You can fetch a list of all card transactions through the card transactions endpoint. This endpoint shows you a list of transactions that have occurred on cards you have issued.

```
curl https://api.allawee.com/card-transactions
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can also fetch a single card transaction by the ID.

```
curl https://api.allawee.com/card-transactions/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
