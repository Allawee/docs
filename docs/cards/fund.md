---
sidebar_position: 3
---

# Fund a card

You can increase a card’s balance by funding it from an account balance. You should call the funding endpoint for this.

```
curl https://api.allawee.com/cards/:id/fund
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "amount": 500,
  "debitSource": "ac.2cbc123456",
  "debitCurrency": "NGN",
  "fxHash": "string"
}'
-X POST
```

| Request Body parameter | Required? | Description |
| :---- | :---- | :---- |
| amount | Yes | The amount of money to increase the card’s balance by. This is also the amount of money that will be deducted from the funding source. |
| debitSource | No | The funding source for the card balance update. |
| debitCurrency | No | The debit currency. |
| fxHash | No | The hash for the conversion. This is only necessary when the debit source and the card have different currencies. |

You should ensure you have enough money in your debit source while funding a card. Otherwise, the attempt will fail.

You can confirm a funding source using the source’s ID.

```js title="Sample Request"
curl https://api.allawee.com/cards/:id/funding-source
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can also check a funding source’s balance:

```js title="Sample Request"
curl https://api.allawee.com/cards/:id/funding-source/balance
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
