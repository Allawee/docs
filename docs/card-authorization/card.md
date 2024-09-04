---
sidebar_position: 1
---

# Card Authorizations

You can fetch a list of all card authorizations through the card authorizations endpoint.

```
curl https://api.allawee.com/card-authorizations
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can also fetch a single card authorization by the ID.

```
curl https://api.allawee.com/card-authorizations/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
