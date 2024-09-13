---
sidebar_position: 2
---

# Activate a card

Once a card has been created, and delivered if it is a physical card, you can activate it with the CVV and a PIN of the cardholder’s choice. The CVV will be on the back of a physical card. You can also check it by fetching the card secrets.

```js title="Sample Request"
curl https://api.allawee.com/cards/:id/activate
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "cvv": "123",
  "pin": "1234"
}'
-X POST
```

After activating the card, you can reset the PIN at any time by passing the new PIN to the reset card PIN endpoint like so:

```js title="Sample Request"
curl https://api.allawee.com/cards/:id/reset-pin
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "pin": "1234"
}'
-X POST
```