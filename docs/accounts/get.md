---
sidebar_position: 3
---

# Get Accounts

You can get accounts you have created, get a particular account through the ID, get an account’s logs, get the logs as a CSV, and get an account’s balance.

You can get all accounts you have created through the get accounts API:

```
curl https://api.allawee.com/accounts
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get a single account like so:

```
curl https://api.allawee.com/accounts/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get an account’s logs, showing you details of actions that have been performed on that account.

```
curl https://api.allawee.com/accounts/:id/logs
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

If you wish to use the logs, you can fetch these logs as a CSV. You can then import the CSV into your systems.

```
curl https://api.allawee.com/accounts/:id/logs/csv
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can fetch an account’s balance through the balance endpoint.

```
curl https://api.allawee.com/accounts/:id/balance
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```