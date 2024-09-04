---
sidebar_position: 5
---

# Get Payments

You can get all payments you’ve made or a single payment. You can also generate a PDF receipt for a payment.

You can get all payments you have made:

```
curl https://api.allawee.com/payments
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get a single payment like so:

```
curl https://api.allawee.com/payments/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can generate a PDF receipt for any payment:

```
curl https://api.allawee.com/payments/:id/generate/pdf
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
