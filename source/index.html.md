---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: false
---

# Introduction

Welcome to the Printerous API! You can use our API to access SweetEscape API endpoints, which you can use to create orders and retrieve order's status.

We have API examples to demonstrate the input and output of the service! You can view code examples in the dark area to the right.

Please replace constant `APIROOT` to these endpoints according to your environment

`Development: http://apitest.printerous.com/`

`Production : https://api.printerous.com/ `


# Authentication

To access other SweetEscape services, you will need to attach a token that identify you as an Authorized User to create shipping address, orders and get order's status related to SweetEscape.

Printerous will give a Releaser Account to SweetEscape, and you need to request the token by signing in using that Releaser Account credentials.

## Get Token


> Output Example:

```json
{
"resp_code": 200,
"resp_status": "success",
"resp_message": "success",
"resp_data":{
"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjE2NjYwLCJpc3MiOiJodHRwOi8vYXBpLnByaW50ZXJvdXMubG9jYWwvc3dlZXRlc2NhcGUvYXV0aC9sb2dpbiIsImlhdCI6MTUxNzgyNzIxMiwiZXhwIjoxNTE4MTg3MjEyLCJuYmYiOjE1MTc4MjcyMTIsImp0aSI6ImZGaDFOclNFNVBhbzFtc1oifQ.-FCy9hJ21sAhN0xgambjfQR7zCy0B6V_ORkpdmDTI7M"
}
```


### HTTP Request

`POST APIROOT/sweetescape/auth/login`

### Query Parameters

Parameter | Mandatory | Default | Description
--------- | --------- | ------- | -----------
email | yes | false | Account Email
password | yes | false | Account Password



# Shipping Address

## Create Shipping Address

> Output Example:

```json
{
  "resp_code": 200,
  "resp_status": "success",
  "resp_message": "success",
  "resp_data": {
      "address": {
          "id:59,
          "address_name": "Office",
          "zip_code": "12240",
          "contact_name": "Johanes Irsan",
          "email": "juliana@printerous.com",
          "phone": "08561471118",
          "country": "Indonesia",
          "province": "DKI Jakarta",
          "city": "Jakarta Selatan",
          "district": "Kebayoran Lama"
      }
  }
}
```

This endpoint create shipping address on Printerous database and returns associated shipping_address_id.

### HTTP Request

`POST APIROOT/sweetescape/shipping_address`

### Query Parameters

Parameter | Mandatory | Type | Description
--------- | --------- | ------- | -----------
token | Yes | Text | Token authentication
address_name | Yes | Varchar(20) | Min length = 3. e.g. Home, Office, dll
contact_name | Yes | Varchar(30) | Min length = 3. e.g. Kevin Osmond, Erick
email | Yes | Varchar(128) | Please send a valid email address
phone | Yes | Varchar(30) | Please send a valid phone number format (we accept " " and "+")
address | Yes | Text | Min length = 10 chars
district_id | Yes | int | id from printerous' ms_districts table
zip_code | Yes | Varchar(10) | Zip Code for shipping address


## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

