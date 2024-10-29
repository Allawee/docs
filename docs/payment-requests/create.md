---
sidebar_position: 2
---

# Create a payment request

You can create a payment request through a call to the Create Payment Request endpoint:

```js title="Sample Request"
curl https://api.allawee.com/payment-requests
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
"method": "bank-transfer",
  "options": {
    "name": "string",
    "bank": "providus"
  },
  "currency": "NGN",
  "amount": 10000,
  "customer": "string",
  "reference": "string",
  "account": "ac.2cbc123456",
  "metadata": {
    "key": "value"
  }
}'
-X POST
```

| Request Body Parameters | Required? | Description |
| :---- | :---- | :---- |
| method | Yes | The payment method, which may be `bank-transfer`, `transfer`, `fx-transfer`, `fx-charge`, `billing`, `local-transfer`. |
| options | Yes | An options object, which should contain a name and may optionally contain a bank for the request. |
| currency | Yes | The payment request currency. |
| amount | Yes | The amount for the request in kobo. |
| customer | No | The customer code for the customer the request is related to. |
| reference | No | A unique reference you can use for payment requests. |
| account | No | The account code for the account the request is being made against. |
| metadata | No | You can include any data you want associated with the request as a metadata. |
