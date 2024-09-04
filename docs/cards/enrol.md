---
sidebar_position: 5
---

# Enrol card for authentication

When a card becomes active, you should enrol the card for authorization through safetokens and 3D Secure (3DS). Safetokens and 3DS are how your customers receive One Time Passcodes (OTPs) to authenticate their online transactions.

You can enrol a card for authentication through safe tokens with the customer’s email and phone number.

```
curl https://api.allawee.com/cards/:id/enroll/safetoken
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "phoneNumber": "+2348123456789",
  "email": "customer@example.com"
}'
-X POST
```

You also use the customer’s email and phone number for 3DS enrollment.

```
curl https://api.allawee.com/cards/:id/enroll/3ds
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-d '{
  "phoneNumber": "+2348123456789",
  "email": "customer@example.com"
}'
-X POST
```

| Request Body parameter | Required? | Description |
| :---- | :---- | :---- |
| phoneNumber | No | The customer’s phone number with the calling code. |
| email | No | The customer’s email. |

The phone number and email provided when setting up the customer the card is assigned to will be the default phone number and email address. However, the default can be overridden by passing a phone number or email during enrollment.
