---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - json

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

> Request Example:

```json
{
  "email":"hello@sweetescapetest.com",
  "password" : "helloworld"
}
```

> Response Example:

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

> Request Example:

```json
{
  "token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjE2NjYwLCJpc3MiOiJodHRwOi8vYXBpLnByaW50ZXJvdXMubG9jYWwvc3dlZXRlc2NhcGUvYXV0aC9sb2dpbiIsImlhdCI6MTUxNzg5MjQ1NiwiZXhwIjoxNTE4MjUyNDU2LCJuYmYiOjE1MTc4OTI0NTYsImp0aSI6Ilc5bE1BeGVrZHpTZm1tdmEifQ.J9_UavavTtx9gV1tGn5sNzZIJyUmuvCfQ8Z6eBxwNE4",
  "address_name":"Office",
  "contact_name":"Vendera Hadi",
  "email":"vendera@printerous.com",
  "phone":"08561471118",
  "address":"Jl. Raya Kebayoran Lama no 333",
  "district_id":"1536",
  "zip_code":"12240"
}
```


> Response Example:

```json
{
  "resp_code": 200,
  "resp_status": "success",
  "resp_message": "success",
  "resp_data": {     
          "id:59,
          "address_name": "Office",
          "zip_code": "12240",
          "contact_name": "Vendera Hadi",
          "email": "vendera@printerous.com",
          "phone": "08561471118",
          "address" : "Jl. Raya Kebayoran Lama no 333",
          "country": "Indonesia",
          "province": "DKI Jakarta",
          "city": "Jakarta Selatan",
          "district": "Kebayoran Lama"    
  }
}
```

This endpoint create shipping address on Printerous database and returns associated shipping_address_id.

### HTTP Request

`POST APIROOT/sweetescape/shipping-addresses`

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
token | Text | Token authentication
address_name | Varchar(20) | Min length = 3. e.g. Home, Office, dll
contact_name | Varchar(30) | Min length = 3. e.g. Kevin Osmond, Erick
email | Varchar(128) | Please send a valid email address
phone | Varchar(30) | Please send a valid phone number format (we accept " " and "+")
address | Text | Min length = 10 chars
district_id | int | id from printerous' ms_districts table
zip_code | Varchar(10) | Zip Code for shipping address

# Orders

## Create Order

This endpoint create SweetEscape's Order on Printerous Platform and returns order information.

<aside class="warning">SEMUA order yang di create melalui service ini akan diproduksi dan ditagihkan ke SweetEscape, pastikan customer betul-betul eligible untuk pembelian tersebut ketika service ini dipanggil</aside>

> Request Example:

```json
{
  "token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjE2NjYwLCJpc3MiOiJodHRwOi8vYXBpLnByaW50ZXJvdXMubG9jYWwvc3dlZXRlc2NhcGUvYXV0aC9sb2dpbiIsImlhdCI6MTUxNzg5MjQ1NiwiZXhwIjoxNTE4MjUyNDU2LCJuYmYiOjE1MTc4OTI0NTYsImp0aSI6Ilc5bE1BeGVrZHpTZm1tdmEifQ.J9_UavavTtx9gV1tGn5sNzZIJyUmuvCfQ8Z6eBxwNE4",
  "shipping_address_id":32,
  "order_details":[
     {
       "sku_code":"sescape_canvas_2030SPR1S",
       "qty":"2",
       "photos":["url_photo_1","url_photo_2"]
     },
     {
       "sku_code":"sescape_photo_4RSP2701S",
       "qty":"8",
       "photos":["url_photo_1","url_photo_2","url_photo_3","url_photo_4"]
     }
  ]
}
```


> Response Example:

```json
{
  "resp_code": 200,
  "resp_status": "success",
  "resp_message": "success",
  "resp_data": {     
          "id:11204,
          "order_no": "PA18205I5NG",
          "status": "Processing",
          "total_price": "Vendera Hadi",
          "shipping_fee": "vendera@printerous.com",
          "final_price": "08561471118",
          "estimated_delivery_date" : "2018-02-14"
          
  }
}
```
### HTTP Request

`POST APIROOT/sweetescape/orders`


### URL Parameters

Parameter | Type | Description
--------- | ---- | -----------
token | Text | Token authentication
shipping_address_id | Integer | 


## Get All Order Statuses


This endpoint returns all sweetescape's orders with their statuses. Result is sorted by created at DESC.

### HTTP Request

`POST APIROOT/sweetescape/orders/statuses`

### URL Parameters

Parameter | Description
--------- | -----------



## Get Specific Order Status(es)


This endpoint returns order(s) with their status respectively. 
Orders specified by order_header_ids on the request parameter.

### HTTP Request

`POST APIROOT/sweetescape/orders/statuses`

### URL Parameters

Parameter | Description
--------- | -----------


