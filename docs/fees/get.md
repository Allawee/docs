---
sidebar_position: 3
---

# Get Fees

You can fetch fees you have created either by getting all fees or by getting a single fee by its ID.

Get all fees:

```
curl https://api.allawee.com/fees
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

Get a single fee by its ID:

```
curl https://api.allawee.com/fees/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
