---
sidebar_position: 4
---

# Merchant Tools

You can use the merchant tools to get all merchants, get available merchant categories, and get one merchant by their ID.

You can get all merchants by calling an endpoint like so:

```
curl https://api.allawee.com/tools/merchants
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get merchant categories:

```
curl https://api.allawee.com/tools/merchants/categories
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get one merchant:

```
curl https://api.allawee.com/tools/merchants/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```