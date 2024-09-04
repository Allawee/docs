---
sidebar_position: 7
---

# Fetch cards and card secrets

You can get all your cards or get a particular card by the ID.

To get all of your cards:

```
curl https://api.allawee.com/cards
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

To get a single card by the card ID:

```
curl https://api.allawee.com/cards/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can also get a card’s secrets:

```
curl https://api.allawee.com/cards/:id/secrets
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
