---
sidebar_position: 3
---

# Update a customer

You can update customer information even after creating the customer. The request body is similar to the request body for creating a new customer. However, it should be a `PUT` request to `https://api.allawee.com/customers/:id` like so:

```js title="Sample Request"
curl https://api.allawee.com/customers/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "name": "string",
  "reference": "customer@example.com",
  "type": "individual",
  "claims": {
    "individualInformation": {
      "title": "string",
      "gender": "M",
      "nationalityCode": "NG",
      "firstName": "string",
      "middleName": "string",
      "lastName": "string",
      "phoneNumber": "+2348123456789",
      "dateOfBirth": "string",
      "email": "customer@example.com"
    },
    "individualAddress": {
      "city": "Yaba",
      "state": "Lagos",
      "countryCode": "NG",
      "addressLineOne": "No 10, Adekunle Close",
      "addressLineTwo": "Off Ciroma Rd"
    },
    "individualIdentity": {
      "type": "bvn",
      "id": "A015BVP13Z",
      "url": "https://example.com/document.png",
      "issuingCountry": "NG"
    },
    "businessInformation": {
      "registrationName": "Good Mill Ltd",
      "phoneNumber": "+2348123456789",
      "email": "goodmill@gmail.com"
    },
    "businessIdentity": {
      "type": "cac",
      "id": "A015BVP13Z",
      "url": "https://example.com/document.png",
      "issuingCountry": "NG"
    },
    "businessDirectors": [
      "string"
    ],
    "businessAddress": {
      "city": "Yaba",
      "state": "Lagos",
      "countryCode": "NG",
      "addressLineOne": "No 10, Adekunle Close",
      "addressLineTwo": "Off Ciroma Rd"
    }
  },
  "verifications": [
    "string"
  ],
  "metadata": {}
}'
-X PUT
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