---
sidebar_position: 5
---

# Get Webhooks

You can get all of your webhooks, get a single webhook, or get a webhook’s secret.

You should call the get all webhooks endpoint to get all of your webhooks.

```
curl https://api.allawee.com/webhooks
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You call the get a single webhook endpoint to get a single webhook with its ID.

```
curl https://api.allawee.com/webhooks/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get a webhook’s signing secret through a call.

```
curl https://api.allawee.com/webhooks/:id/secret
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```