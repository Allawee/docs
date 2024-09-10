---
sidebar_position: 2
---

# Creating a Dispute

You can create a dispute on a transaction through the Create Dispute endpoint:

```
curl https://api.allawee.com/disputes
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "reason": "value-not-received",
  "source": "c.auth.2cbc123456",
  "text": "I did not receive my order",
  "documents": [
    "https://s3.amazonaws.com/..."
  ],
  "user": "usr.2cbc123456"
}'
-X POST
```

| Request Body Parameters | Required? | Description |
| :---- | :---- | :---- |
| reason | Yes | The reason can be one of four values: `fraudulent`, `duplicate`, `value-not-received`, and `general`. |
| source | Yes | The authorization code of the transaction being disputed. |
| text | No | Details of the dispute. |
| documents | No | An array of links related to the dispute, which may serve as evidence. |
| user | No | The user code of the user involved. |
