---
sidebar_position: 3
---

# Getting Card Programs

You can get all your card programs or get a particular card program by the ID.

To get all of your card programs:

```
curl https://api.allawee.com/card-programs
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

To get a single card program by the program ID:

```
curl https://api.allawee.com/card-programs/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```