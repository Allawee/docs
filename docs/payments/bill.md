---
sidebar_position: 3
---

# Make a bill payment

You can make a bill payment, such as payment for airtime or electricity, through the bill payment endpoint.

```
curl https://api.allawee.com/payments/bill
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "product": "bp.2cbc123456",
  "inputs": {
 "phoneNumber": "08055429186",
 "amount": "40000"
},
  "customer": "string",
  "reference": "string",
  "debitSource": "ac.2cbc123456",
  "metadata": {
    "key": "value"
  }
}'
-X POST
```

| Request Body Parameters | Required? | Description |
| :---- | :---- | :---- |
| product | Yes | The bill product code of the bill you wish to pay for. |
| inputs | Yes | Information regarding the bill you want to pay for, such as phone number and provider for airtime purchase. |
| customer | No | The customer code for the bill, if a customer has been set up. |
| reference | No | A unique reference you can use to track the bill. |
| debitSource | No | The account code of the account that should be debited for the bill. |
| metadata | No | Any extra information you wish to associate with the bill. |

You can validate a bill after creating it:

```
curl https://api.allawee.com/payments/bill/validate
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "product": "bp.2cbc123456",
  "inputs": {
    "phoneNumber": "08055429186",
    "amount": "40000"
 },
  "customer": "string",
  "reference": "string",
  "debitSource": "ac.2cbc123456",
  "metadata": {
    "key": "value"
  }
}'
-X POST
```
