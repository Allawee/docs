---
sidebar_position: 2
---

# FX Tools

You can use the FX tools to work with foreign exchange.

You can get rates:

```
curl https://api.allawee.com/tools/fx/rates
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get the current USD rate:

```
curl https://api.allawee.com/tools/fx/rates?from=USD&to=NGN
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can set your fx quote when converting between currencies:

```
curl https://api.allawee.com/tools/fx/quotes
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "from": "NGN",
  "to": "USD",
  "amount": 1100
}'
-X POST
```

| Request Body Parameters | Required? | Description |
| :---- | :---- | :---- |
| from | Yes | The currency the quote is a conversion from. |
| to | Yes | The currency the quote is a conversion to. |
| amount | Yes | The amount of the “to” currency you want. If the amount is 1100, the “from” value is NGN, and the “to” value is “USD”, the quote would be for a purchase of $11. |

