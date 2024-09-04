---
sidebar_position: 4
---

# Account Deposit Channels

You can add deposit channels for accounts you create and update the account names of the deposit channels you create for those accounts. Adding a deposit channel means an account’s balance can be credited through that channel. Only bank account payments are currently supported as a deposit channel for an account.

You can add a deposit channel for an account like so:

```
curl https://api.allawee.com/accounts/:id/deposit-channels
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "type": "bank-account",
}'
-X POST
```

You can also update the deposit channel account name like so:

```
curl https://api.allawee.com/accounts/:id/deposit-channels/update-account-name
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "type": "bank-account",
  “accountNumber”: “string”
}'
-X PUT
```
