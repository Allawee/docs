---
sidebar_position: 2
---

# Get your customers

You can get all of your customers or get a particular customer by their ID.

To get all of your customers:

```
curl https://api.allawee.com/customers
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

To get a single customer by their customer ID:

```
curl https://api.allawee.com/customers/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```