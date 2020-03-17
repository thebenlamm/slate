---
title: FraudFix API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - footer

search: true
---

# Introduction

Welcome to the FraudFix JSON API. Use this API to easily and securely submit new orders and to check on existing orders.

To use the FraudFix API, you must have an API key. Visit our website [FraudFix.com](https://fraudfix.com/) for more information.

# Authentication

FraudFix uses API keys to grant access to its API. Your API key should be included in the header of all API requests in the following format:

`X-API-Key: your_api_key`

<aside class="notice">
Remember to replace <code>your_api_key</code> with your personal API key.
</aside>

# Orders

## Submit an Order

```shell
curl https://api.fraudfix.com/order \
  -X POST \
  -H 'Content-Type: application/json' \
  -H "X-API-Key: your_api_key" \
  -d '{
        "orderNumber": "12345",
        "siteName": "MY-SITE-NAME",
        "grandTotal": 49.99,
        "orderDate": "2020-03-17T12:43:59-05:00",
        "customerId": "54321",
        "loginName": "dvader",
        "loginPassword": "Skywa1ker"
  }'
```

```javascript
const axios = require('axios');
axios.post('https://api.fraudfix.com/order', 
    {
        "orderNumber": "12345",
        "siteName": "MY-SITE-NAME",
        "grandTotal": 49.99,
        "orderDate": "2020-03-17T12:43:59-05:00",
        "customerId": "54321",
        "loginName": "dvader",
        "loginPassword": "Skywa1ker"
    },
    {
    headers: {'X-API-Key': 'your_api_key'}
    });
```

> Example Response

``` 
202 Accepted
```

Submit an order to our fraud engines to be analyzed and graded.

### Request

`POST https://api.fraudfix.com/order`

You must include API KEY in the header of the POST request. The POST /order endpoint lets you submit a single order for analysis. A successful POST returns the FraudFix OrderId in the Location header.

### Parameters

Name | Type | Required | Description
--------- | ---- | -------- | -----------
<code>orderNumber</code> | string | Required | 
<code>siteName</code> | string | Required | 
<code>grandTotal</code> | number | Required | 
<code>orderDate</code> | datetime | Required | 
<code>customerId</code> | string | Optional | 
<code>loginName</code> | string | Optional | 
<code>loginPassword</code> | string | Optional |               
<code>billing</code> | [AddressInfo](#address) | Optional | 
<code>shipping</code> | [AddressInfo](#address) | Optional | 

### Response
Status | Meaning
------ | -------
202 | Accepted for processing
400 | Bad request
401 | Unauthorized

## Get an order

```shell
curl "https://api.fraudfix.com/order/1234" /
  -H "X-API-Key: your_api_key"
```

```javascript
const axios = require('axios');
axios.get('https://api.fraudfix.com/order/1234', 
    { headers: {'X-API-Key': 'your_api_key'} }
    );
```

> The above command returns JSON structured like this:

```json
{
  "orderId": 1234,
  "score": 2,
  "insured": "Y"
}
```

This endpoint retrieves the status of a specific order


### Request

`GET https://api.fraudfix.com/<orderId>`

### URL Parameters

Name | Description
--------- | -----------
<code>orderId</code> | The orderId returned from the POST order api

### Response
Status | Meaning
------ | -------
200 | OK
401 | Unauthorized
404 | Not Found

## Order Schemas

### AddressInfo

### Properties
Name | Type | Required | Description
--------- | ---- | -------- | -----------
<code>firstName</code> | string | Optional | 
<code>middleName</code> | string | Optional | 
<code>lastName</code> | string | Optional | 
<code>company</code> | string | Optional |
<code>address1</code> | string | Required | 
<code>address2</code> | string | Optional |
<code>city</code> | string | Optional | 
<code>state</code> | string | Optional | 
<code>country</code> | string | Required | two character country code
<code>zip</code> | string | Optional | 
<code>eveningPhone</code> | string | Optional | 
<code>dayPhone</code> | string | Optional | 
<code>cellPhone</code> | string | Optional | 
<code>email</code> | string | Optional | 