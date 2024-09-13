---
sidebar_position: 3
---

# Get Accounts

You can get accounts you have created, get a particular account through the ID, get an account’s logs, get the logs as a CSV, and get an account’s balance.

You can get all accounts you have created through the get accounts API:

```js title="Sample Request"
curl https://api.allawee.com/accounts
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": [
        {
            "status": "active",
            "name": "Baggy App",
            "type": "main",
            "currency": "NGN",
            "depositChannels": [
                {
                    "type": "bank-account",
                    "accountName": "Baggy App",
                    "accountNumber": "0062622048",
                    "bankName": "Allawee Sandbox Bank",
                    "bankCode": "000",
                    "partner": "allawee-sandbox",
                    "createdAt": "2023-03-09T10:18:45.604Z",
                    "updatedAt": "2023-03-09T10:18:45.604Z"
                }
            ],
            "createdAt": "2023-03-09T10:18:45.605Z",
            "updatedAt": "2023-03-09T10:18:45.605Z",
            "id": "ac.2tVZczWw7m6Teoeb7",
            "object": "account"
        }
    ],
    "metadata": {
        "hasMore": false
    }
}
```

You can get a single account like so:

```js title="Sample Request"
curl https://api.allawee.com/accounts/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": {
        "status": "active",
        "name": "Baggy App",
        "type": "main",
        "currency": "NGN",
        "depositChannels": [
            {
                "type": "bank-account",
                "accountName": "Baggy App",
                "accountNumber": "0062622048",
                "bankName": "Allawee Sandbox Bank",
                "bankCode": "000",
                "partner": "allawee-sandbox",
                "createdAt": "2023-03-09T10:18:45.604Z",
                "updatedAt": "2023-03-09T10:18:45.604Z"
            }
        ],
        "createdAt": "2023-03-09T10:18:45.605Z",
        "updatedAt": "2023-03-09T10:18:45.605Z",
        "id": "ac.2tVZczWw7m6Teoeb7",
        "object": "account"
    }
}
```

You can get an account’s logs, showing you details of actions that have been performed on that account.

```js title="Sample Request"
curl https://api.allawee.com/accounts/:id/logs
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

If you wish to use the logs, you can fetch these logs as a CSV. You can then import the CSV into your systems.

```js title="Sample Request"
curl https://api.allawee.com/accounts/:id/logs/csv
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can fetch an account’s balance through the balance endpoint.

```js title="Sample Request"
curl https://api.allawee.com/accounts/:id/balance
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```