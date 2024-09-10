---
sidebar_position: 2
---

# Update Webhooks

You can update a webhook after creating it.

```
curl https://api.allawee.com/webhooks/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "name": "string",
  "events": [
    "card.authorization.request"
  ],
  "apiVersion": "2023-02-01",
  "description": "string",
  "url": "string",
  "metadata": {}
}'
-X PUT
```

You can change all of the values used to create the webhook except the signing key.