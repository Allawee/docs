---
sidebar_position: 5
---

# Bill Tools

You can use the bills tools endpoint to get bill categories, get all bill products, and get one bill product.

You can get all bill categories like so:

```js title="Sample Request"
curl https://api.allawee.com/tools/bills/categories
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get all bill products:

```js title="Sample Request"
curl https://api.allawee.com/tools/bills/products
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get one bill product:

```js title="Sample Request"
curl https://api.allawee.com/tools/bills/products/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
