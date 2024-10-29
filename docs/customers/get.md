---
sidebar_position: 2
---

# Get your customers

You can get all of your customers or get a particular customer by their ID.

To get all of your customers:

```js title="Sample Request"
curl https://api.allawee.com/customers
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": [
        {
            "name": "Ciroma C Adekunle",
            "type": "individual",
            "status": "active",
            "claims": {
                "individualInformation": {
                    "firstName": "Ciroma",
                    "lastName": "Adekunle",
                    "middleName": "Chukwuma",
                    "email": "ciroma@gmail.com",
                    "phoneNumber": "+2349154109234",
                    "title": "Mr",
                    "gender": "M",
                    "dateOfBirth": "1997-2-13",
                    "nationalityCode": "NG"
                },
                "individualAddress": {
                    "city": "Yaba",
                    "state": "NG-LA",
                    "countryCode": "NG",
                    "addressLineOne": "100 herbert macaulay road",
                    "addressLineTwo": "",
                    "postalCode": "11041"
                },
                "individualIdentity": {
                    "type": "bvn",
                    "id": "22489035167",
                    "issuingCountry": "NG"
                }
            },
            "verifications": [
                {
                    "type": "tier-2",
                    "status": "verified"
                }
            ],
            "metadata": {
                "userId": 2345
            },
            "createdAt": "2023-03-14T23:21:12.882Z",
            "updatedAt": "2023-03-14T23:21:12.882Z",
            "id": "cus.2tXNjMhytgx7hCxu9",
            "object": "customer"
        },
        {
            "name": "Iyanu Deborah Oluwole",
            "type": "individual",
            "status": "active",
            "claims": {
                "individualInformation": {
                    "firstName": "Iyanu",
                    "lastName": "Oluwole",
                    "middleName": "Deborah",
                    "email": "amos+1@allawee.com",
                    "phoneNumber": "+2349154109237",
                    "title": "Miss",
                    "gender": "F",
                    "dateOfBirth": "1996-02-14",
                    "nationalityCode": "NG"
                },
                "individualAddress": {
                    "city": "mainland",
                    "state": "NG-LA",
                    "countryCode": "NG",
                    "addressLineOne": "44 commercial road",
                    "addressLineTwo": null,
                    "postalCode": "100001"
                },
                "individualIdentity": {
                    "type": "bvn",
                    "id": "22478937481",
                    "issuingCountry": "NG"
                }
            },
            "verifications": [
                {
                    "type": "tier-2",
                    "status": "verified"
                }
            ],
            "metadata": {
                "userId": "1234"
            },
            "createdAt": "2023-03-09T10:24:10.108Z",
            "updatedAt": "2023-03-10T21:49:57.535Z",
            "id": "cus.2tVZh8GkvSJu6xgRJ",
            "object": "customer"
        }
    ],
    "metadata": {
        "hasMore": false
    }
}
```

To get a single customer by their customer ID:

```js title="Sample Request"
curl https://api.allawee.com/customers/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

```js title="Sample Success Response"
{
    "code": "success",
    "data": {
        "name": "Ciroma C Adekunle",
        "type": "individual",
        "status": "active",
        "claims": {
            "individualInformation": {
                "firstName": "Ciroma",
                "lastName": "Adekunle",
                "middleName": "Chukwuma",
                "email": "ciroma@gmail.com",
                "phoneNumber": "+2349154109234",
                "title": "Mr",
                "gender": "M",
                "dateOfBirth": "1997-2-13",
                "nationalityCode": "NG"
            },
            "individualAddress": {
                "city": "Yaba",
                "state": "NG-LA",
                "countryCode": "NG",
                "addressLineOne": "100 herbert macaulay road",
                "addressLineTwo": "",
                "postalCode": "11041"
            },
            "individualIdentity": {
                "type": "bvn",
                "id": "22489035167",
                "issuingCountry": "NG"
            }
        },
        "verifications": [
            {
                "type": "tier-3",
                "status": "verified"
            }
        ],
        "metadata": {
            "userId": 2345
        },
        "createdAt": "2023-03-14T23:21:12.882Z",
        "updatedAt": "2023-03-16T02:03:49.738Z",
        "id": "cus.2tXNjMhytgx7hCxu9",
        "object": "customer"
    }
}
```