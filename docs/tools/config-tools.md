---
sidebar_position: 3
---

# Configuration Tools

You can use the configuration tools endpoints to set payment configurations that apply as defaults to all your requests. Payment configurations you can set include your pay-in account, your pay-out account, and your fees for bank transfers and bill payments.

To get your configuration:

```js title="Sample Request"
curl https://api.allawee.com/tools/configuration
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

To update your configuration:

```js title="Sample Request"
curl https://api.allawee.com/tools/configuration/payment
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "payInAccount": "ac.2cbc123456",
  "payOutAccount": "ac.2cbc123456",
  "fees": {
    "bankTransfer": "fee.2cbc123456",
    "billPayment": "fee.2cbc123456"
  }
}'
-X PUT
```

| Request Body Parameters | Required? | Description |
| :---- | :---- | :---- |
| payInAccount | No | This is the account you should use to receive payments for your Allawee business. |
| payOutAccount | No | This is the default account that is debited for your transfers. |
| fees | No | These are the default fees that apply to your bank transfers and bill payments. You can pass `bankTransfer` and `billPayment` fees. |