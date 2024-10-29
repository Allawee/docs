---
sidebar_position: 2
---

# Make a transfer payment

We provide a transfer API that you can use to make payouts to Nigerian bank accounts. You can make payments with a single call to the payout endpoint.

```js title="Sample Request"
curl https://api.allawee.com/payments/payouts
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "method": "bank-transfer",
  "options": {
    "method": "bank-transfer",
    "accountNumber": "string",
    "bankCode": "string",
    "narration": "string",
    "note": "string",
    "destination": "ac.2cbc123456",
    "fxCurrency": "NGN",
    "fxQuoteHash": "string"
  },
  "currency": "NGN",
  "amount": 10000,
  "customer": "string",
  "reference": "string",
  "fee": "fee.2cbc123456",
  "debitSource": "ac.2cbc123456",
  "metadata": {
    "key": "value"
  }
}'
-X POST
```

| Request Body Parameter | Required? | Description |
| :---- | :---- | :---- |
| method | Yes | The transfer method. Payment methods can be `bank-transfer`, `transfer`, `fx-transfer`, `fx-charge`, `billing`, and `local-transfer`. |
| options | Yes | Details regarding the recipient account for the payment. |
| currency | Yes | The transfer currency, which may be NGN or USD. |
| amount | Yes | The transfer amount in the lowest unit of the currency, which will be kobo for NGN transactions. |
| customer | No | The customer code for the transfer, if the customer has been set up using the customer endpoint. |
| reference | No | A unique reference for the payment. |
| fee | No | A fee code that should be applied to the payment. You can only use this if you have set up a fee. |
| debitSource | No | The account code for the account the payment should be debited from. The default is your main account. |
| metadata | No | Any data you wish to store. |
