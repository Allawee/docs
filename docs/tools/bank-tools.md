---
sidebar_position: 1
---

# Bank Tools

The bank tools let you work with banks and account numbers. You can get all banks you can make payments to, get the likely bank an account number belongs to, and resolve an account number and bank code combination.

You can use the get banks endpoint to get a list of all banks:

```
curl https://api.allawee.com/tools/banks
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can get a list of banks an account number likely belongs to. This endpoint uses the Central Bank of Nigeria’s checksum to determine the account number’s likely bank. However, you should bear in mind that while these are the likely banks, it is possible for the actual bank to be missing from the list. This is due to non-compliance with the CBN’s recommended account number checksum by some financial institutions.

```
curl https://api.allawee.com/tools/banks/short-list/:accountNumber
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

You can resolve an account number, getting the account name through the account number and bank code if the account details are valid. If not, your request fails.

```
curl https://api.allawee.com/tools/banks/resolve?accountNumber=1234567890&bankCode=058
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```
