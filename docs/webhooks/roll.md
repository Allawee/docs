---
sidebar_position: 4
---

# Roll Webhook Signing Secret

You can roll a webhook’s signing secret to change the signing key. This is the ideal way to update a webhook’s signing secret.

```js title="Sample Request"
curl https://api.allawee.com/webhooks/:id/secret/roll
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "signingKey": "string"
}'
-X POST
```
