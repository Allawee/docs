---
sidebar_position: 1
---

# How Authorization Works

## Authorization Check Request

When the card network request for card balance and card holder name; Allawee sends a `card.authorization.request` with type `check`, you should respond with either an `approve` or `decline` action.

If you respond with an `approve` you should also respond with `cardBalance` (amount in minor) and `cardHolderName`, unless the response would be invalid and authorization `declined`

### Authorization Capture Request

When the card network request for a debit on a card for a purchase; Allawee checks if the card, customer and account are all active. If they are all active an `authorization` is created. If either, card, customer or account is inactive, request is completely discarded.

Next Allawee performs more pre-checks on the account, checks if the funding source has enough balance and checks if spending controls on the card allows the authorization.

If checks fails, Allawee automatically decline the authorization and send you a `card.authorization.closed` event. If checks succeeds, Allawee holds the funds in reserve and sends you a `card.authorization.request` with type `capture`. You should respond to the request with either an `approve` or `decline` action.

If you respond with an `approve` you should go ahead and lock the user funds. After your response, the `authorization` object is updated and a `card.authorization.closed` is sent with the new status.

On receiving the new `card.authorization.closed` event, if the authorization object status is set to `approved`, you should debit the user funds. Otherwise if authorization object is set to `decline` you should release the user money from the lock back to their available balance.

### Authorization with updated amount

In a case where there is an update on the amount to debit, we would set the authorization object to `pending` and send you a `card.authorization.update` event that should be responded with an action within 4 seconds.

You should compare the authorization object new amount with the locked amount and available balance. For-example if new amount is greater than locked amount plus user balance, you should `decline` with an `insufficient-funds` code and release currently locked funds.

If new amount is less than locked amount or new amount + locked amount is less than user balance. you should `approve` and debit new amount.

### Authorization Reversals

When card network triggers a reversal, we would send a `card.authorization.update` event with authorization object updated to `reversed` and credit your settlement balance with the reversed amount. You should proceed to reverse the user funds.

_NOTE_:

- Authorization Events sent via `card.authorization.request`, `card.authorization.closed` and `card.authorization.update` events, are required for card authorizations.
- Authorization Events with authorization object status set to `pending` are only sent once and there is a timeout of 4 seconds, after which your `timeoutDefault` response is applied.
- Authorization Events with authorization object status set to either `approved`, `declined` or `reversed` can be resent multiple times until you respond with a 200 HTTP StatusCode. You should implement a way to track duplicated transactions in-case event is resent.

## Responding to authorization requests

Authorization response should be sent as JSON responses with the following parameters.

| Field name | Required or optional | Type | Description |
| --- | --- | --- | --- |
| action | required | `approve`, `decline` | Authorization action to be taken |
| code | optional | `account-not-found`, `account-inactive`, `insufficient-funds`, `invalid-transaction`, `duplicate-transaction` | Reason for `decline` action; this would be added to the authorization object, for referencing |
| cardBalance | optional (_required for authorization check requests_) | Integer | The card's balance is represented in the lowest unit of the currency. e.g 100000 kobo for NGN1,000 or 1000000 cents for USD$10,000 |
| cardHolderName | optional | String | Name of the card holder, e.g John Doe |
| metadata | optional | Set of key-value pairs | Key-value pair of any information you would like to add to the object's metadata, which you can later retrieved later. |

- Here is an example for `card.authorization.closed`, it is similar to `card.authorization.request` but comes with final status of the authorization object

```js title="Sample"
{
  "event": "card.authorization.closed",
  "data": {
    "amount": 50000,
    "card": "c.2tUYkKGqPTWH3ZtM4",
    "channel": "online",
    "createdAt": "2023-03-14T18:22:51.000Z",
    "currency": "NGN",
    "decisionType": "direct-response",
    "fees": 6500,
    "id": "c.auth.2tXJoWXy2NZNFU9mY",
    "networkData": {
      "cardAcceptorNameLocation": "MATRIX ENERGY LIMITE LA LANG",
      "cardAccountNumber": "0140881806",
      "network": "verve",
      "reference": "1678818170917",
      "rrn": "1678802924287",
      "stan": "1678802924287"
    },
    "object": "card.authorization",
    "status": "approved",
    "type": "capture"
  },
  "metadata": {
    "sentAt": "2023-03-14T18:26:54.528995Z",
    "event": "evt.2tXJoYkRayFK8H9Eq"
  }
}
```

- Here is a sample for `card.authorization.update` it is similar to `card.authorization.request` but comes with the new status of the authorization object, e.g reversed

```js title="Sample"
{
  "event": "card.authorization.update",
  "data": {
    "amount": 500,
    "card": "c.2tUYkKGqPTWH3ZtM4",
    "channel": "online",
    "createdAt": "2023-03-13T03:36:12.000Z",
    "currency": "NGN",
    "decisionType": "direct-response",
    "id": "c.auth.2tWnAbJMupWGmnjTC",
    "networkData": {
      "cardAcceptorNameLocation": "MATRIX ENERGY LIMITE LA LANG",
      "network": "verve",
      "reference": "1678678572421"
    },
    "object": "card.authorization",
    "status": "reversed",
    "type": "capture"
  },
  "metadata": {
    "sentAt": "2023-03-13T03:37:05.16974Z",
    "event": "evt.2tWnBFgxzBn1HqEvr"
  }
}
```

- Here is a sample for `card.transaction.created`, this is event is sent when an actual transaction is created.

```js title="Sample"
{
  "event": "card.transaction.created",
  "data": {
    "amount": -50000,
    "authorization": "c.auth.2tXJVgE6Z4vX97RRj",
    "card": "c.2tUYkKGqPTWH3ZtM4",
    "channel": "online",
    "createdAt": "2023-03-14T17:59:32.000Z",
    "currency": "NGN",
    "customer": "cus.2tUZALBt23So88JZm",
    "fees": -6500,
    "id": "c.txn.2tXJVhhjbU3pPekQb",
    "networkData": {
      "cardAcceptorNameLocation": "MATRIX ENERGY LIMITE LA LANG",
      "network": "verve",
      "reference": "1678816769131",
      "rrn": "1678802924287",
      "stan": "1678802924287"
    },
    "object": "card.transaction",
    "type": "capture"
  },
  "metadata": {
    "sentAt": "2023-03-14T17:59:33.657411Z",
    "event": "evt.2tXJVhhjbU3pPekQd"
  }
}
```
