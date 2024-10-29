---
sidebar_position: 4
---

# Resend Payment Events

You can requeue a payment if it failed:

```js title="Sample Request"
curl https://api.allawee.com/payments/:id/requeue
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{}'
-X POST
```

You can also request to have the event for a completed payment resent:

```js title="Sample Request"
curl https://api.allawee.com/payments/:id/resend-events/payment-completed
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{}'
-X POST
```
