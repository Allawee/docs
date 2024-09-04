---
sidebar_position: 1
---

# Create a customer

Customers are how the API links resources, such as cards or bank accounts, to the holder. You need to create customers before you can issue cards or assign bank accounts. You can create a customer like so:

```
curl https://api.allawee.com/customers
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
-X POST
```

| Request Body parameter | Required? | Description |
| :---- | :---- | :---- |
| name | Yes | The customer’s legal name. If it is a business, it should be the business’s registration name. |
| reference | Yes | A unique reference for the customer. It could be the ID you use to identify the customer within your system or an email. |
| type | Yes | This value should be either `individual` or `business` and identifies whether the customer is a natural person or a business entity. |
| claims | Yes | This field contains the customer’s KYC information. |
| verifications | Yes | This represents the verification tier of the customer. It may be `tier-1`, `tier-2`, or `tier-3`. |
| metadata | Yes | This is an object value you can use to store any values you wish to associate with the customer. |
