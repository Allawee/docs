---
sidebar_position: 3
---

# Update a customer

You can update customer information even after creating the customer. The request body is similar to the request body for creating a new customer. However, it should be a `PUT` request to `https://api.allawee.com/customers/:id` like so:

```
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