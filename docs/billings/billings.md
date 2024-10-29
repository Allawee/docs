---
sidebar_position: 1
---

# Billings

You can get all of your billings or get a single billing by its ID. These are your billings for your use of Allawee’s services.

To get all of your billings:

```js title="Sample Request"
curl https://api.allawee.com/billings
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

To get a single billing by its ID:

```js title="Sample Request"
curl https://api.allawee.com/billings/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
