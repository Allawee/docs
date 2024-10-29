---
sidebar_position: 2
---

# Create a Fee

You should call the Create fees endpoint to create a fee:

```js title="Sample Request"
curl https://api.allawee.com/fees
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "name": "string",
  "description": "string",
  "structure": "flat",
  "currency": "NGN",
  "value": 500,
  "cap": 10000,
  "account": "ac.2cbc123456",
  "metadata": {
    "key": "value"
  }
}'
-X POST
```

| Request Body Parameters | Required? | Description |
| :---- | :---- | :---- |
| name | Yes | A name for the fee to identify it. |
| description | No | A description of the fee. |
| structure | Yes | \`flat\` or \`percentage\`, which determines whether it is a flat fee or a percentage fee. |
| currency | No | The currency for the fee. |
| value | Yes | The percentage if the selected structure is a percentage fee and the fee in the smallest unit of the currency if it is a flat fee. |
| cap | No | An optional limit on the fee if it is a percentage fee. |
| account | Yes | The account the fee should be paid into. |
| metadata | No | Any other information you wish to associate with the fee. |
