---
sidebar_position: 3
---

# Update Disputes

You can update the optional fields of a dispute after creating it. The optional fields include the text, document, and user.

```
curl https://api.allawee.com/disputes/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "text": "I did not receive my order",
  "documents": [
    "https://s3.amazonaws.com/..."
  ],
  "user": "usr.2cbc123456"
}'
-X PUT
```

You can also close a dispute:

```
curl https://api.allawee.com/disputes/:id/close
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{}'
-X PUT
```