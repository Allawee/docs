---
sidebar_position: 2
---

# Get Events

To get all of your events, you should call the get events endpoint:

```js title="Sample Request"
curl https://api.allawee.com/events
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can also get a single event with the event ID:

```js title="Sample Request"
curl https://api.allawee.com/events/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```