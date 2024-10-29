---
sidebar_position: 1
---

# Create Webhooks

The webhook you set while creating your account is the default webhook for all webhook events. However, you can create a webhook for specific events.

```js title="Sample Request"
curl https://api.allawee.com/webhooks
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
  "signingKey": "string",
  "metadata": {}
}'
-X POST
```

| Request Body Parameter | Required? | Description |
| :---- | :---- | :---- |
| name | Yes | The name of the webhook. |
| events | Yes | The events that the webhook should be called for, |
| apiVersion | No | The api version the webhook is for. |
| description | No | A description of the webhook. |
| url | Yes | The webhook url. |
| signingKey | No | This is the key Allawee will send in requests to help you verify that it is from Allawee. |
| metadata | No | Any data you wish to associate with the webhook. |
