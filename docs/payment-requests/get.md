---
sidebar_position: 2
---

# Get payment requests

You can get either all of your payment requests or a single payment request by the ID.

To get all of your payment requests:

```
curl https://api.allawee.com/payment-requests
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get a single payment request like so:

```
curl https://api.allawee.com/payment-requests/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
