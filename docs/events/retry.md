---
sidebar_position: 3
---

# Retry Events

You can retry events with their IDs to have them resent to your webhook.

```
curl https://api.allawee.com/events/:id/retry
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{}'
-X POST
```
