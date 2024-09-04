---
sidebar_position: 2
---

# Create an account

You can use the create account endpoint to create an account for a business or individual. The types of accounts you can create include “main”, “sub”, and “virtual” accounts. An important difference is that virtual accounts cannot hold value, and any payment made to a virtual account usually ends up in a main account. This makes virtual accounts ideal when you want to create different payment channels that end up in a single collection account where you can access the funds. These accounts can only receive NIP transfers.

Your request to create an account should look like so:

```
curl https://api.allawee.com/accounts
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "name": "string",
  "settlementAccount": "string",
  "reference": "string",
  "customer": "string",
  "currency": "NGN",
  "type": "main",
  "depositChannels": [
    "bank-account"
  ],
  "metadata": {}
}'
-X POST
```

| Request Body Parameter | Required? | Description |
| :---- | :---- | :---- |
| name | Yes | The account name. When a name enquiry is performed on the account, this is the account name that will show up. |
| settlementAccount | No | This should be present for virtual accounts, and is the settlement account where the funds are deposited after payments come in. |
| reference | No | Account reference |
| customer | No | A customer identifier. |
| currency | Yes | This shows the account currency. It should either be `NGN` or `USD`. |
| type | Yes | The account type should be `main`, `sub`, or `virtual`. |
| depositChannels | No | The channel for deposits. This currently only supports `bank-account` deposits. |
| metadata | No | Any metadata you wish to associate with the card. |
