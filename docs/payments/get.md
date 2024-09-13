---
sidebar_position: 5
---

# Get Payments

You can get all payments you’ve made or a single payment. You can also generate a PDF receipt for a payment.

You can get all payments you have made:

```js title="Sample Request"
curl https://api.allawee.com/payments
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": [
        {
            "amount": 1000000,
            "currency": "NGN",
            "status": "failed",
            "type": "pay-out",
            "account": "ac.2w6gycf9ZNQNRes3H",
            "fundingSource": "ac.2w6gycf9ZNQNRes3H",
            "method": "bank-transfer",
            "methodData": {
                "bankTransfer": {
                    "accountNumber": "0000000000",
                    "bankCode": "000013",
                    "bankName": "GUARANTY TRUST BANK",
                    "accountName": "JOHN DOE",
                    "sourceAccountName": "Test",
                    "narration": "test payment"
                }
            },
            "fees": 2688,
            "createdAt": "2024-09-13T13:51:47.400Z",
            "updatedAt": "2024-09-13T13:51:47.575Z",
            "failureReason": "insufficient-funds",
            "events": [
                "evt.2wcj2CVUpNZGXXxsC"
            ],
            "feeBreakdown": [
                {
                    "amount": 2688,
                    "group": "platform",
                    "type": "platform-fees"
                }
            ],
            "id": "p.2wcj2CxxhnpcWAc4z",
            "object": "payment"
        }
    ],
    "metadata": {
        "hasMore": false
    }
}
```

You can get a single payment like so:

```js title="Sample Request"
curl https://api.allawee.com/payments/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": {
        "amount": 1000000,
        "currency": "NGN",
        "status": "failed",
        "type": "pay-out",
        "account": "ac.2w6gycf9ZNQNRes3H",
        "fundingSource": "ac.2w6gycf9ZNQNRes3H",
        "method": "bank-transfer",
        "methodData": {
            "bankTransfer": {
                "accountNumber": "0000000000",
                "bankCode": "000013",
                "bankName": "GUARANTY TRUST BANK",
                "accountName": "JOHN DOE",
                "sourceAccountName": "Test",
                "narration": "test payment"
            }
        },
        "fees": 2688,
        "createdAt": "2024-09-13T13:51:47.400Z",
        "updatedAt": "2024-09-13T13:51:47.575Z",
        "failureReason": "insufficient-funds",
        "events": [
            "evt.2wcj2CVUpNZGXXxsC"
        ],
        "feeBreakdown": [
            {
                "amount": 2688,
                "group": "platform",
                "type": "platform-fees"
            }
        ],
        "id": "p.2wcj2CxxhnpcWAc4z",
        "object": "payment"
    }
}
```

You can generate a PDF receipt for any payment:

```js title="Sample Request"
curl https://api.allawee.com/payments/:id/generate/pdf
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
