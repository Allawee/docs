---
sidebar_position: 3
---

# Enable and Disable webhooks

You have to enable a webhook for it to take effect and stop sending event webhooks to the default.

```
curl https://api.allawee.com/webhooks/:id/enable
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{}'
-X POST
```

You can also disable a webhook, after which it falls back to the default webhook.

```
curl https://api.allawee.com/webhooks/:id/disable
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{}'
-X POST
```
