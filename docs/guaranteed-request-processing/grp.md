---
sidebar_position: 1
---

# Guaranteed Request Processing (GRP)

Guaranteed request processing is a delayed processing system in the Allawee API.When a request cannot be processed immediately, there is a status code of 202 and a response code of `request-accepted`. You can also access the request ID in the response header you get, with a `x-request-id` key.

When the request is processed, you get a webhook notification with an event type of `request-completed`. You can also check the status of your request using the ID:

```
curl https://api.allawee.com/requests/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

The GRP feature is controlled by the API key you use to authorise your request. When you create an authorisation token, the GRP option is off by default, but you can toggle it on. If you leave it off, your requests will fail fast when they cannot be processed.
