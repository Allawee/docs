---
sidebar_position: 1
slug: /
---

# Introduction

Learn to use the Allawee API to issue cards, assign bank accounts to your customers, make transfers, and pay bills.

## Getting Started

Welcome to the Allawee API documentation, where you’ll learn to issue payment cards and bank accounts through APIs and your Allawee dashboard.

## Base URL

The base url for requests to allawee is api.allawee.com. However, where the action being performed is a secure action, the base url for such requests will be secure.allawee.com. Data from secure requests are handled differently to protect sensitive information.

### Setting up an account

You can sign up for an Allawee business account at: [https://infra.allawee.com/signup](https://infra.allawee.com/signup). This account is necessary to obtain API keys and begin issuing cards. We will also need your business information, such as registration documents, as part of the compliance process. However, even before your business KYC documents are approved, you can test the Issuing API.

## Support

You can reach Allawee Support through email: [support@allawee.com](mailto:support@allawee.com).

You can also access the [Allawee Public Postman collection](https://www.postman.com/allaweeinc/allawee-infra/collection/gc64xzz/allawee-v2023-02-01?action=share&creator=2932477).

## Authentication and Authorization

Allawee maintains granular permissions, allowing you to determine what each Access Key you generate can do.

To generate a new Access Key, you should check the “API Keys” section. You will then see a button to generate a new Access Key. You should give your key a name that helps you distinguish it from all other keys, while also including the API address you will be using when you make requests from the key. You can determine the permissions of every key you create by toggling the permission scopes. If you want the key you will be using within your core app service to have all permissions, you can toggle all of the fields. However, if you wanted to share a limited access Key with a partner, you may choose to toggle only some of the fields.

At the top right of your dashboard, you can toggle between test mode and live mode. This determines whether you will create a test key or a live key. The version of the API you will be calling is also determined by your key. You can see your key’s version in the “version” column after creating it. Creating a new API key always uses the most recent version.

Note: You can only view an access key when you create it. You cannot view it subsequently, and so you should store it safely.

You use your Access Keys to authenticate and authorise your API calls. You should use the key as a Bearer token, setting your request’s “Authorization” header to “Bearer \{\{accessToken}}”.

You can revoke your keys from the API Keys section, using the delete icon for the associated key.

## Response Structures

### Response status codes

Allawee’s API is a RESTful API. When a request is successful, the response will be 2XX, within the 200 to 209 range. When there is a request error, it will be 4XX. For example, 400 is a bad request, 401 is an unauthenticated request, and 403 is a forbidden request. 5XX responses signify server errors.

If your request cannot be processed immediately, but will still be processed, you will get a 202 response. You can check the section on Guaranteed Request Processing (GRP) for more details on this.

### Pagination

The Allawee API is paginated when fetching a range of data. You can use query parameters to specify the page and the limit for each page. The first page is 0. The limit specifies the number of entries that should be within a page. In your response, there will be a `pagination` key that carries pagination data for your request. `lastId` is the ID of the last entry in that response, limit is the number of entries in the response, and count is the total number of entries in the database for your request.

### Parameter expansion

Where data is relational, and the response will typically be an ID, you can expand the ID into the full data object. You can use the `expand` query parameter for this, specifying the key you wish to expand.

### Filtering

You can filter API data with the `filter` query parameter. The filter value consists of three parts - the key you wish to filter by, the comparison operator to use, and the value to compare against, all separated by pipes. As an example, a filter value could be `cardType||EQ||verve`. This filter value will ensure that the response only contains entries where the cardType is equal to verve. Other comparison operators are LIKE, IN, NIN, and NEQ.

### Sorting

You can sort the response data with the `sort` query parameter. This allows you to determine the key that should be used when your response is being sorted. By default, your response will be sorted by the date the entries were created, with the most recent being at the top. However, you can change this order by setting the key you wish to use as the sort value. You can put a minus sign in front of the key to alter the sort direction. If you set the value as `amount`, it would be sorted in ascending value, with the lowest amounts coming first. However, if you set the value as `-amount`, it would be sorted in descending order, with the highest amounts coming first.

### Select

You can use the `select` query parameter to get only some key values in your response. This can reduce the size of the JSON you get as a response. You can do this by including the keys you wish to get back in an array as the value of the `select` query parameter.

## Guaranteed Request Processing (GRP)

Guaranteed request processing is a delayed processing system in the Allawee API.When a request cannot be processed immediately, there is a status code of 202 and a response code of `request-accepted`. You can also access the request ID in the response header you get, with a `x-request-id` key.

When the request is processed, you get a webhook notification with an event type of `request-completed`. You can also check the status of your request using the ID:

```js title="Sample Request"
curl https://api.allawee.com/requests/:id
-H "Authorization: Bearer YOUR_SECRET_KEY"
-H "Content-Type: application/json"
-X GET
```

The GRP feature is controlled by the API key you use to authorise your request. When you create an authorisation token, the GRP option is off by default, but you can toggle it on. If you leave it off, your requests will fail fast when they cannot be processed.
