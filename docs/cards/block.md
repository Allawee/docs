---
sidebar_position: 8
---

# Block, Unblock, and Terminate cards

You can block, unblock, and terminate cards you have created and activated.

You can block a card like so:

```
curl https://api.allawee.com/cards/:id/block
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X POST
```

When you block a card, you can undo the action by unblocking the card.

```
curl https://api.allawee.com/cards/:id/unblock
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X POST
```

However, terminating a card is a permanent action.

```
curl https://api.allawee.com/cards/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X DELETE
```
