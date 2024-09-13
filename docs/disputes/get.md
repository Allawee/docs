---
sidebar_position: 4
---

# Get Disputes

To get all disputes you have created:

```js title="Sample Request"
curl https://api.allawee.com/disputes
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get a single dispute like so:

```js title="Sample Request"
curl https://api.allawee.com/disputes/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```