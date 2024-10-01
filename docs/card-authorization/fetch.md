---
sidebar_position: 2
---

# Get Card Authorizations

You can fetch a list of all card authorizations through the card authorizations endpoint.

```js title="Sample Request"
curl https://api.allawee.com/card-authorizations
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": [
        {
            "decisionType": "system-response",
            "fees": 0,
            "status": "declined",
            "type": "check",
            "amount": 0,
            "reserved": false,
            "currency": "NGN",
            "channel": "atm",
            "card": "c.2tVghquVL5LxCkjB3",
            "networkData": {
                "cardAcceptorNameLocation": "EMERALD",
                "stan": "5DJJ0614624HSJ",
                "rnn": "6e9007747be67838",
                "txnReference": "5951474897",
                "requestBody": {
                    "requestId": "615e7666-6e90-42e5-bedf-07747be67838",
                    "amount": 0,
                    "walletId": "0153781018",
                    "transactionReference": "5951474897",
                    "mac": "4b6b2ba7e49eb7200e2df0c56a365d5bbf81a945e17559be06b6a5fc5093ac94e6e9c88a087868040a5a85c81d06d71168491114455965948bcc95dfdb585ca9",
                    "acquiringInstitutionId": "50614624",
                    "terminalId": "10332838",
                    "terminalType": "02",
                    "merchantId": "1033283801649  ",
                    "currencyCode": "566",
                    "cardAcceptorNameLocation": "EMERALD HOTEL ATM 9    LAGOS        KNNG",
                    "transactionDateTime": "2023-02-22T11:24:39"
                },
                "responseBody": {
                    "amount": 100000,
                    "mac": "825186b67868d91736daf74604c7332ba244aea235e7ba08cd0b83609d1a168588b3f4244d7a1de5769cf010d6bbd5723f24123fcf3619398af14095cc7c89a7",
                    "name": "John Doe",
                    "requestId": "615e7666-6e90-42e5-bedf-07747be67838",
                    "responseCode": "45",
                    "transactionReference": "5951474897"
                }
            },
            "statusReason": "timeout-error",
            "createdAt": "2023-03-10T22:03:49.298Z",
            "updatedAt": "2023-03-10T22:03:53.614Z",
            "id": "c.auth.2tW3sESJQ4ZW9DKSG",
            "object": "card.authorization"
        }
    ],
    "metadata": {
        "hasMore": false
    }
}
```

You can also fetch a single card authorization by the ID.

```js title="Sample Request"
curl https://api.allawee.com/card-authorizations/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": {
        "decisionType": "system-response",
        "fees": 0,
        "status": "declined",
        "type": "check",
        "amount": 0,
        "reserved": false,
        "currency": "NGN",
        "channel": "atm",
        "card": "c.2tVghquVL5LxCkjB3",
        "networkData": {
            "cardAcceptorNameLocation": "EMERALD",
            "stan": "5DJJ0614624HSJ",
            "rnn": "6e9007747be67838",
            "txnReference": "5951474897",
            "requestBody": {
                "requestId": "615e7666-6e90-42e5-bedf-07747be67838",
                "amount": 0,
                "walletId": "0153781018",
                "transactionReference": "5951474897",
                "mac": "4b6b2ba7e49eb7200e2df0c56a365d5bbf81a945e17559be06b6a5fc5093ac94e6e9c88a087868040a5a85c81d06d71168491114455965948bcc95dfdb585ca9",
                "acquiringInstitutionId": "50614624",
                "terminalId": "10332838",
                "terminalType": "02",
                "merchantId": "1033283801649  ",
                "currencyCode": "566",
                "cardAcceptorNameLocation": "EMERALD HOTEL ATM 9    LAGOS        KNNG",
                "transactionDateTime": "2023-02-22T11:24:39"
            },
            "responseBody": {
                "amount": 100000,
                "mac": "825186b67868d91736daf74604c7332ba244aea235e7ba08cd0b83609d1a168588b3f4244d7a1de5769cf010d6bbd5723f24123fcf3619398af14095cc7c89a7",
                "name": "John Doe",
                "requestId": "615e7666-6e90-42e5-bedf-07747be67838",
                "responseCode": "45",
                "transactionReference": "5951474897"
            }
        },
        "statusReason": "timeout-error",
        "createdAt": "2023-03-10T22:03:49.298Z",
        "updatedAt": "2023-03-10T22:03:53.614Z",
        "id": "c.auth.2tW3sESJQ4ZW9DKSG",
        "object": "card.authorization"
    }
}
```
