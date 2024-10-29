---
sidebar_position: 3
---

# Simulation

You can simulate actions in test mode that usually aren’t within your control in live mode.

## Card Programs Simulation

You can simulate a card program going live.

```js title="Sample Request"
curl https://api.allawee.com/simulation/card-programs/:id/go-live
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{}'
-X POST
```

## Cards Simulation

You can simulate several steps in a card authorization flow.

You can simulate sending the card authorization request check.

```js title="Sample Request"
curl https://api.allawee.com/simulation/cards/:id/request-authorization/check
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "channel": "atm",
  "mcc": "string",
  "merchantDescriptor": "string"
}'
-X POST
```

| Request Body Parameter | Required? | Description |
| :---- | :---- | :---- |
| channel | Yes | The payment channel. This can be \`atm\`, \`pos\`, \`online\`, or \`in-app\`. |
| mcc | No | The merchant’s MCC. |
| merchantDescriptor | No | The merchant’s name and location. |

You can simulate sending the card authorization request capture.

```js title="Sample Request"
curl https://api.allawee.com/simulation/cards/:id/request-authorization/capture
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "amount": 0,
  "fees": 0,
  "channel": "atm",
  "mcc": "string",
  "merchantDescriptor": "string"
}'
-X POST
```

| Request Body Parameter | Required? | Description |
| :---- | :---- | :---- |
| amount | Yes | The transaction amount to be debited from the card. |
| fees | Yes | The transaction fee to be debited from the card. |
| channel | Yes | The payment channel. This can be \`atm\`, \`pos\`, \`online\`, or \`in-app\`. |
| mcc | No | The merchant’s MCC. |
| merchantDescriptor | No | The merchant’s name and location. |

You can simulate updating the card authorization request capture.

```js title="Sample Request"
curl https://api.allawee.com/simulation/cards/:id/request-authorization/update-capture
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "amount": 0,
  "fees": 0,
  "updateAmount": 0,
  "updateFees": 0,
  "channel": "atm",
  "mcc": "string",
  "merchantDescriptor": "string"
}'
-X POST
```

| Request Body Parameter | Required? | Description |
| :---- | :---- | :---- |
| amount | Yes | The transaction amount to be debited from the card. |
| fees | Yes | The transaction fee to be debited from the card. |
| updateAmount | Yes | Update the transaction amount to be debited from the card. |
| updateFees | Yes | Update the transaction fee to be debited from the card. |
| channel | Yes | The payment channel. This can be \`atm\`, \`pos\`, \`online\`, or \`in-app\`. |
| mcc | No | The merchant’s MCC. |
| merchantDescriptor | No | The merchant’s name and location. |

You can simulate sending a card authorization request reverse capture.

```js title="Sample Request"
curl https://api.allawee.com/simulation/cards/:id/request-authorization/reverse-capture
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "amount": 0,
  "fees": 0,
  "channel": "atm",
  "mcc": "string",
  "merchantDescriptor": "string"
}'
-X POST
```

## Payments Simulation

You can simulate receiving a bank transfer payment.

```js title="Sample Request"
curl https://api.allawee.com/simulation/payments/pay-in
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "method": "string",
  "accountNumber": "0123456789"
}'
-X POST
```

| Request Body Parameter | Required? | Description |
| :---- | :---- | :---- |
| method | Yes | The payment method. |
| accountNumber | Yes | The recipient account number. |