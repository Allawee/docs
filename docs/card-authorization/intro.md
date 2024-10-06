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

- Here is an example for `Authorization` Implementation.

```go title="Example Authorization Implementation in Go"
package main

import (
	"crypto/hmac"
	"crypto/sha512"
	"encoding/hex"
	"encoding/json"
	"github.com/kataras/iris/v12"
)

var AllaweeWebhookSigningKey = "XXXXXXXXXXX"

type AllaweeEventBody struct {
	Event    string                   `json:"event"`
	Data     AllaweeAuthorizationData `json:"data"`
	Metadata AllaweeEventBodyMetadata `json:"metadata"`
}

type AllaweeAuthorizationData struct {
	Card          string                          `json:"card"`
	Type          string                          `json:"type"`
	Id            string                          `json:"id"`
	Amount        int64                           `json:"amount"`
	Fees          int64                           `json:"fees"`
	Channel       string                          `json:"channel"`
	Reserved      bool                            `json:"reserved"`
	NetworkData   AllaweeEventBodyDataNetworkData `json:"networkData"`
	CreatedAt     time.Time                       `json:"createdAt"`
	Status        string                          `json:"status"`
	DeclineReason string                          `json:"declineReason"`
	DecisionType  string                          `json:"decisionType"`
	Currency      string                          `json:"currency"`
}

type AllaweeEventBodyDataNetworkData struct {
	Rrn                      string `json:"rrn"`
	Stan                     string `json:"stan"`
	Network                  string `json:"network"`
	TxnReference             string `json:"txnReference"`
	CardAcceptorNameLocation string `json:"cardAcceptorNameLocation"`
}

type AllaweeEventBodyMetadata struct {
	CreatedAt time.Time `json:"createdAt"`
	Event     string    `json:"event"`
}

// Verify the request by comparing HMAC Hex of the webhook signing key
func verifyRequest(c iris.Context) *AllaweeEventBody {
	signature := c.Request().Header.Get("Allawee-Signature")
	reqBody, _ := c.GetBody()

	hash := hmacHashHex(AllaweeWebhookSigningKey, string(reqBody))

	if hash != signature {
		c.StopWithJSON(iris.StatusBadRequest, iris.Map{"error": "Invalid Signature"})
		return nil
	}

	// Get TransferEventBody
	var body AllaweeEventBody
	err := json.Unmarshal(reqBody, &body)
	if err != nil {
		c.StopWithJSON(iris.StatusBadRequest, iris.Map{"error": "Invalid Request"})
		return nil
	}

	return &body
}


func hmacHashHex(key string, secret string) string {
	h := hmac.New(sha512.New, []byte(key))
	h.Write([]byte(secret))
	return hex.EncodeToString(h.Sum(nil))
}

func main(c iris.Context) {
	body := verifyRequest(c)
	if body == nil {
		return
	}

	if body.Event == "card.authorization.request" {
		response := processRequest(body)
		c.JSON(response)
		return
	}

	if body.Event == "card.authorization.closed" {
		response := processClosed(body)
		c.JSON(response)
		return
	}

	if body.Event == "card.authorization.update" {
		response := processUpdate(body)
		c.JSON(response)
		return
	}

	if body.Event == "card.transaction.created" {
		response := iris.Map{"code": "success"}
		c.JSON(response)
		return
	}

	c.StopWithJSON(iris.StatusBadRequest, iris.Map{"error": "Invalid Request"})
	return
}

func processRequest(body *AllaweeEventBody) iris.Map {
	if body.Data.Type == "check" {
		return processCheck(body)
	}

	if body.Data.Type == "capture" {
		return processCapture(body)
	}

	return iris.Map{"action": "decline", "metadata": iris.Map{"reason": "Invalid Request"}}
}

func processCheck(body *AllaweeEventBody) iris.Map {
	// Get the card's wallet
	wallet := getCardWallet(body.Data.Card)
	if wallet == nil {
		return iris.Map{"action": "decline", "code": "account-not-found"}
	}

	if !wallet.Active {
		return iris.Map{"action": "decline", "code": "account-inactive"}
	}

	return iris.Map{
		"action":         "approve",
		"cardBalance":    wallet.AvailableBalance,
		"cardHolderName": wallet.Name,
	}
}

func processCapture(body *AllaweeEventBody) iris.Map {
	// Get the card's wallet
	wallet := getCardWallet(body.Data.Card)

	// if the wallet is not active, decline
	if wallet == nil {
		return iris.Map{"action": "decline", "code": "account-not-found"}
	}

	// if the wallet is not active, decline
	if !wallet.Active {
		return iris.Map{"action": "decline", "code": "account-inactive"}
	}

	// Check if transaction already exists, using authorization id as reference
	transaction := getTransaction(body.Data.Id)
	if transaction != nil {
		return iris.Map{"action": "decline", "code": "duplicate-transaction"}
	}

	// Get transaction fees, in-case you are adding a fee (optional)
	transactionFee, err := calculateTransactionFee(body.Data.Amount)
	if err != nil {
		return iris.Map{"action": "decline"}
	}

	if wallet.AvailableBalance < (body.Data.AmountAndFees() + *transactionFee) {
		return iris.Map{"action": "decline", "code": "insufficient-funds"}
	}

	// Add a step to verify your internal spending controls (optional)
	if err := checkSpendingControl(body, wallet, *transactionFee); err != nil {
		return iris.Map{"action": "decline", "code": "spending-control"}
	}

	// Place a lien on the account, note the transaction is not yet final until closed,
	// so you want to only reserve the money, optionally pass in the transactionFee to reserve also
	if err := placeLien(body, wallet, *transactionFee); err != nil {
		return iris.Map{"action": "decline"}
	}

	return iris.Map{"action": "approve"}
}

// processClosed processes authorization closed event
// This is called when an authorization is closed on allawee
func processClosed(body *AllaweeEventBody) iris.Map {
	// Get Original Transaction
	originalTransaction := getTransaction(body.Data.Id)
	if originalTransaction == nil {
		return iris.Map{"action": "decline", "code": "invalid-transaction"}
	}

	// get card's wallet
	wallet := getCardWallet(body.Data.Card)
	if wallet == nil {
		return iris.Map{"action": "decline", "code": "account-not-found"}
	}

	if body.Data.Status == "approved" {
		return processAuthorizationApproved(body, wallet, originalTransaction)
	}

	if body.Data.Status == "declined" {
		return processAuthorizationDeclined(body, wallet, originalTransaction)
	}

	return iris.Map{"action": "decline", "code": "invalid-transaction"}
}

// processAuthorizationUpdate processes authorization updated event
// This is called when an authorization is updated on allawee, in case where a new amount is to be captured or it is completely reversed
func processUpdate(body *AllaweeEventBody) iris.Map {
	// Get Original Transaction
	originalTransaction := getTransaction(body.Data.Id)
	if originalTransaction == nil {
		return iris.Map{"action": "decline", "code": "invalid-transaction"}
	}

	// get card's wallet
	wallet := getCardWallet(body.Data.Card)
	if wallet == nil {
		return iris.Map{"action": "decline", "code": "account-not-found"}
	}

	if body.Data.Status == "pending" {
		return processAuthorizationPending(body, wallet, originalTransaction)
	}

	if body.Data.Status == "reversed" {
		return processAuthorizationReversed(body, wallet, originalTransaction)
	}

	return iris.Map{"action": "decline", "code": "invalid-transaction"}

}

func processAuthorizationApproved(
	body *AllaweeEventBody,
	wallet *Wallet,
	originalTransaction *Transaction) iris.Map {

	if originalTransaction.Status != "pending" {
		return iris.Map{"action": "decline", "code": "duplicate-transaction"}
	}

	// Debit the lien that was previously reserved
	if err := processDebitLien(body, wallet, originalTransaction); err != nil {
		return iris.Map{"action": "decline"}
	}

	return iris.Map{"action": "approve"}
}

func processAuthorizationPending(
	body *AllaweeEventBody,
	wallet *Wallet,
	originalTransaction *Transaction) iris.Map {

	if originalTransaction.Status != "pending" {
		return iris.Map{"action": "decline", "code": "duplicate-transaction"}
	}

	// Get transaction fees
	transactionFee, err := calculateTransactionFee(body.Data.Amount)
	if err != nil {
		return iris.Map{"action": "decline"}
	}

	// if new amount is greater than the original amount and the wallet do not have a sufficient balance for the new amount
	// then reverse the money reserved and return an insufficient-funds error
	// Note: NetworkAmountAndFees here mean the original amount and fees that was sent excluding your own additional fee if applied
	if (body.Data.AmountAndFees() > originalTransaction.NetworkAmountAndFees()) && ((wallet.AvailableBalance + originalTransaction.NetworkAmountAndFees()) < (body.Data.AmountAndFees() + *transactionFee)) {
		if err := processReverseLien(body, wallet, originalTransaction); err != nil {
			return iris.Map{"action": "decline"}
		}

		return iris.Map{"action": "decline", "code": "insufficient-funds"}
	}

	//  debit lien with new amount
	if err := processDebitLien(body, wallet, originalTransaction, *transactionFee); err != nil {
		return iris.Map{"action": "decline"}
	}

	return iris.Map{"action": "approve"}

}

// in a case where a previous pending authorization was declined, remove the reserved funds and return to the user
func processAuthorizationDeclined(
	body *AllaweeEventBody,
	wallet *Wallet,
	originalTransaction *Transaction) iris.Map {

	if originalTransaction.Status != "pending" {
		return iris.Map{"action": "decline", "code": "duplicate-transaction"}
	}

	if err := processReverseLien(body, wallet, originalTransaction); err != nil {
		return iris.Map{"action": "decline"}
	}

	return iris.Map{"action": "approve"}
}

// in a case where a previous successful authorization was reversed by the network, refund user and return the cash to the user
func processAuthorizationReversed(
	body *AllaweeEventBody,
	wallet *Wallet,
	originalTransaction *Transaction) iris.Map {

	if originalTransaction.Status != "success" {
		return iris.Map{"action": "decline", "code": "invalid-transaction"}
	}

	// Note: NetworkAmountAndFees here mean the original amount and fees that was sent excluding your own additional fee if applied
	if originalTransaction.NetworkAmountAndFees() != body.Data.AmountAndFees() {
		return iris.Map{"action": "decline", "code": "invalid-transaction"}
	}

	// Notice processReverse here is different from processReverseLien, as the money is no longer in lien
	if err := processReverse(body, wallet, originalTransaction); err != nil {
		return iris.Map{"action": "decline"}
	}

	return iris.Map{"action": "approve"}
}
```

```ts title="Example Authorization Implementation in TypeScript"
import { createHmac } from "crypto";

const AllaweeWebhookSigningKey = "XXXXXXXXXXX";

interface AllaweeEventBody {
  event: string;
  data: AllaweeAuthorizationData;
  metadata: AllaweeEventBodyMetadata;
}

interface AllaweeAuthorizationData {
  card: string;
  type: string;
  id: string;
  amount: number;
  fees: number;
  channel: string;
  reserved: boolean;
  networkData: AllaweeEventBodyDataNetworkData;
  createdAt: Date;
  status: string;
  declineReason: string;
  decisionType: string;
  currency: string;
}

interface AllaweeEventBodyDataNetworkData {
  rrn: string;
  stan: string;
  network: string;
  txnReference: string;
  cardAcceptorNameLocation: string;
}

interface AllaweeEventBodyMetadata {
  createdAt: Date;
  event: string;
}

interface Wallet {
  active: boolean;
  availableBalance: number;
  name: string;
}

interface Transaction {
  status: string;
  networkAmountAndFees: number;
}

async function hmacHashHex(
  key: string,
  secret: string,
  algorithm = "sha512",
): Promise<string> {
  return createHmac(algorithm, key).update(secret).digest("hex");
}

// Verify the request by comparing HMAC Hex of the webhook signing key
async function verifyRequest(signature: string, rawBody: string) {
  const hash = await hmacHashHex(AllaweeWebhookSigningKey, rawBody);

  if (hash != signature) {
    throw new Error("Invalid Signature");
  }
}

function main(body: AllaweeEventBody) {
  const signature = "xxxx";
  const rawBody = "xxxx";

  verifyRequest(signature, rawBody);

  if (body.event == "card.authorization.request") {
    return processRequest(body);
  }

  if (body.event == "card.authorization.closed") {
    return processClosed(body);
  }

  if (body.event == "card.authorization.update") {
    return processUpdate(body);
  }

  if (body.event == "card.transaction.created") {
    // save transaction
    return { code: "success" };
  }

  return { error: "Invalid Request" };
}

function processRequest(body: AllaweeEventBody) {
  if (body.data.type == "check") {
    return processCheck(body);
  }

  if (body.data.type == "capture") {
    return processCapture(body);
  }

  return { action: "decline", metadata: { reason: "Invalid Request" } };
}

function processCheck(body: AllaweeEventBody) {
  // Get the card's wallet
  const wallet = getCardWallet(body.data.card);
  if (!wallet) {
    return { action: "decline", code: "account-not-found" };
  }

  if (!wallet.active) {
    return { action: "decline", code: "account-inactive" };
  }

  return {
    action: "approve",
    cardBalance: wallet.availableBalance,
    cardHolderName: wallet.name,
  };
}

async function processCapture(body: AllaweeEventBody) {
  // Get the card's wallet
  const wallet = getCardWallet(body.data.card);

  // if the wallet is not active, decline
  if (!wallet) {
    return { action: "decline", code: "account-not-found" };
  }

  // if the wallet is not active, decline
  if (!wallet.active) {
    return { action: "decline", code: "account-inactive" };
  }

  // Check if transaction already exists, using authorization id as reference
  const transaction = getTransaction(body.data.id);
  if (!transaction) {
    return { action: "decline", code: "duplicate-transaction" };
  }

  // Get transaction fees, in-case you are adding a fee (optional)
  const transactionFee = calculateTransactionFee(body.data.amount);

  if (
    wallet.availableBalance <
    body.data.amount + body.data.fees + transactionFee
  ) {
    return { action: "decline", code: "insufficient-funds" };
  }

  // Add a step to verify your internal spending controls (optional)
  if (!checkSpendingControl(body, wallet, transactionFee)) {
    return { action: "decline", code: "spending-control" };
  }

  // Place a lien on the account, note the transaction is not yet final until closed,
  // so you want to only reserve the money, optionally pass in the transactionFee to reserve also
  try {
    await placeLien(body, wallet, transactionFee);
  } catch (e) {
    return { action: "decline" };
  }

  return { action: "approve" };
}

// processClosed processes authorization closed event
// This is called when an authorization is closed on allawee
function processClosed(body: AllaweeEventBody) {
  // Get Original Transaction
  const originalTransaction = getTransaction(body.data.id);
  if (!originalTransaction) {
    return { action: "decline", code: "invalid-transaction" };
  }

  // get card's wallet
  const wallet = getCardWallet(body.data.card);
  if (!wallet) {
    return { action: "decline", code: "account-not-found" };
  }

  if (body.data.status == "approved") {
    return processAuthorizationApproved(body, wallet, originalTransaction);
  }

  if (body.data.status == "declined") {
    return processAuthorizationDeclined(body, wallet, originalTransaction);
  }

  return { action: "decline", code: "invalid-transaction" };
}

// processAuthorizationUpdate processes authorization updated event
// This is called when an authorization is updated on allawee, in case where a new amount is to be captured or it is completely reversed
function processUpdate(body: AllaweeEventBody) {
  // Get Original Transaction
  const originalTransaction = getTransaction(body.data.id);
  if (!originalTransaction) {
    return { action: "decline", code: "invalid-transaction" };
  }

  // get card's wallet
  const wallet = getCardWallet(body.data.card);
  if (!wallet) {
    return { action: "decline", code: "account-not-found" };
  }

  if (body.data.status == "pending") {
    return processAuthorizationPending(body, wallet, originalTransaction);
  }

  if (body.data.status == "reversed") {
    return processAuthorizationReversed(body, wallet, originalTransaction);
  }

  return { action: "decline", code: "invalid-transaction" };
}

async function processAuthorizationApproved(
  body: AllaweeEventBody,
  wallet: Wallet,
  originalTransaction: Transaction,
) {
  if (originalTransaction.status != "pending") {
    return { action: "decline", code: "duplicate-transaction" };
  }

  // Debit the lien that was previously reserved
  try {
    await processDebitLien(body, wallet, originalTransaction);
  } catch (e) {
    return { action: "decline" };
  }

  return { action: "approve" };
}

async function processAuthorizationPending(
  body: AllaweeEventBody,
  wallet: Wallet,
  originalTransaction: Transaction,
) {
  if (originalTransaction.status != "pending") {
    return { action: "decline", code: "duplicate-transaction" };
  }

  // Get transaction fees
  const transactionFee = calculateTransactionFee(body.data.amount);

  // if new amount is greater than the original amount and the wallet do not have a sufficient balance for the new amount
  // then reverse the money reserved and return an insufficient-funds error
  // Note: NetworkAmountAndFees here mean the original amount and fees that was sent excluding your own additional fee if applied
  if (
    body.data.amount + body.data.fees >
      originalTransaction.networkAmountAndFees &&
    wallet.availableBalance + originalTransaction.networkAmountAndFees <
      body.data.amount + body.data.fees + transactionFee
  ) {
    try {
      await processReverseLien(body, wallet, originalTransaction);
    } catch (e) {
      return { action: "decline" };
    }

    return { action: "decline", code: "insufficient-funds" };
  }

  //  debit lien with new amount
  try {
    await processDebitLien(body, wallet, originalTransaction, transactionFee);
  } catch (e) {
    return { action: "decline" };
  }

  return { action: "approve" };
}

// in a case where a previous pending authorization was declined, remove the reserved funds and return to the user
async function processAuthorizationDeclined(
  body: AllaweeEventBody,
  wallet: Wallet,
  originalTransaction: Transaction,
) {
  if (originalTransaction.status != "pending") {
    return { action: "decline", code: "duplicate-transaction" };
  }

  try {
    await processReverseLien(body, wallet, originalTransaction);
  } catch (e) {
    return { action: "decline" };
  }

  return { action: "approve" };
}

// in a case where a previous successful authorization was reversed by the network, refund user and return the cash to the user
async function processAuthorizationReversed(
  body: AllaweeEventBody,
  wallet: Wallet,
  originalTransaction: Transaction,
) {
  if (originalTransaction.status != "success") {
    return { action: "decline", code: "invalid-transaction" };
  }

  // Note: NetworkAmountAndFees here mean the original amount and fees that was sent excluding your own additional fee if applied
  if (
    originalTransaction.networkAmountAndFees !=
    body.data.amount + body.data.fees
  ) {
    return { action: "decline", code: "invalid-transaction" };
  }

  // Notice processReverse here is different from processReverseLien, as the money is no longer in lien

  try {
    await processReverse(body, wallet, originalTransaction);
  } catch (e) {
    return { action: "decline" };
  }

  return { action: "approve" };
}

function getCardWallet(cardId: string): Wallet {
  return {} as Wallet;
}

function getTransaction(transactionId: string): Transaction {
  return {} as Transaction;
}

function calculateTransactionFee(amount: number): number {
  return 200;
}

function checkSpendingControl(
  body: AllaweeEventBody,
  wallet: Wallet,
  transactionFee: number,
): boolean {
  return true;
}

function processDebitLien(
  body: AllaweeEventBody,
  wallet: Wallet,
  originalTransaction: Transaction,
  transactionFee?: number,
) {
  throw new Error("Function not implemented.");
}
function processReverseLien(
  body: AllaweeEventBody,
  wallet: Wallet,
  originalTransaction: Transaction,
) {
  throw new Error("Function not implemented.");
}

function processReverse(
  body: AllaweeEventBody,
  wallet: Wallet,
  originalTransaction: Transaction,
) {
  throw new Error("Function not implemented.");
}

function placeLien(
  body: AllaweeEventBody,
  wallet: Wallet,
  transactionFee: number,
) {
  throw new Error("Function not implemented.");
}
```

### Simulation

You can use our simulation APIs in test mode to simulate sending an authorization events (via https://elements.getpostman.com/redirect?entityId=19364408-149559f1-606a-40dd-b230-c9d81dcf3bde&entityType=collection or using the dashboard).

#### Sample Authorization Check Request Success Response

```json
{ "action": "approve", "cardBalance": 50000, "cardHolderName": "John Doe" }
```

#### Sample Authorization Decline Response

```json
{ "action": "decline", "code": "insufficient-funds" }
```

#### Sample Authorization Approve Response

```json
{
  "action": "approve",
  "metadata": { "acme-transaction-reference": "0C1202321234" }
}
```
