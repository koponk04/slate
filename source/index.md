---
title: Kaskus API Reference

language_tabs:
  - php

toc_footers:
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>
  - <a href='http://kasdok.mooo.com'>Improved version of Kasdok</a>

search: true
---

# Introduction

Welcome to the Kaskus API! You can use our API to access Kaskus API endpoints

## Getting Started

This is general guide on how to use Kaskus API. 
Kaskus api base URI is located in https://www.kaskus.co.id/api/oauth (without trailing slash) and will be refered as BASE_URI in example and detailed guide. 
Module available will be listed in sidebar located on left side of the page (sorted alphabetically).

The API is RESTful. Data is exposed in the form of URIs that represent resources and can be fetched with HTTP clients (like web browsers).
 
 
Most of the API use OAuth based authentication, so it does honor "Authorization" header (and it is required to include in most request).

`Authorization: Oauth 1 signature`
 
Data returned in the response message is provided in two formats, the default format is XML and another is JSON . 
To make a request which return certain data types you can use a query string or request header.


query string

`/uri?output=json`

request header 

`Return-Type: text/json`


## SDK

Kaskus SDK For PHP

This repository contains the open source PHP SDK that allows you to access Kaskus API from your PHP app.

This version of the Kaskus SDK for PHP requires
 
* PHP 5.4 or greater.
* Composer

Installation
------------

1. Require this library in your composer.json
2. [Composer](https://getcomposer.org/) is a prerequisite for using Kaskus Sdk for PHP. Install composer globally, then run `composer install` to install required files.
3. Get Consumer Key and Consumer Secret for your application.
4. Require `vendor/autoload.php` in your application.
5. Follow sample script for further usage

```json
{
  "require": {
    "kaskus/kaskus-php-sdk": "v0.2.0"
  }
}
```

Usage
-----

Minimal example:

```php
<?php

// skip these two lines if you use composer 
define('KASKUS_SDK_SRC_DIR', '/path/to/kaskus-sdk-for-php/src/Kaskus/');
require __DIR__ . '/path/to/kaskus-sdk-for-php/autoload.php';

// skip this line if you do not use composer
require 'vendor/autoload.php';

$consumerKey = 'YOUR_API_KEY';
$consumerSecret = 'YOUR_API_SECRET';

$client = new \Kaskus\KaskusClient($consumerKey, $consumerSecret);

try {
    $response = $client->get('v1/hot_threads');
    $forumList = $response->json();
    print_r($forumList);
} catch (\Kaskus\Exceptions\KaskusRequestException $exception) {
    // Kaskus Api returned an error
    
} catch (\Exception $exception) {
    // some other error occured
    
}

```

Login With Kaskus Oauth
-----------------

Use this [Oauth sample](https://github.com/kaskus/kaskus-php-sdk/blob/master/sample/oauth_sample.php)

Login With Kaskus xAuth
-----------------

This is only for Kaskus internal apps.

## Login

Login with username and password to directly get access token

### HTTP Request

`POST /authentication`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
user|Username kaskus|username
pass|md5 of your password|0cc175b9c0f1b6a831c399e269772661

## Logout

Logout

### HTTP Request

`DELETE /authentication`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------




Advance Usage
-------------

We use guzzle as HTTP Client, for further usage, read [Guzzle](http://guzzle.readthedocs.org/en/latest/)


Oauth 2 (BETA)
-----------------

Now we can also use Oauth 2 to access Kaskus API

## Issue Access Token

Issue Access Token

### HTTP Request

`POST https://www.kaskus.co.id/oauth/access-token`

Parameter | Description | Example
--------- | ----------- | -----------

Field | Description | Example
--------- | -----------| -----------
grant_type | required, it can be one of these values: `client_credentials`, `password`, `refresh_token` | client_credentials
client_id | required, client id that given to you | YOUR_CLIENT_ID
client_secret | required, client secret that given to you | YOUR_CLIENT_SECRET
scope | optional, list of scope with comma as delimiter | thread.read,thread.write
username | only required for password grant | USERNAME
password | only required for password grant, raw password | USER_PASSWORD
refresh_token | only required for refresh_token grant, use refresh_token returned when you issue access token with `password` grants or `refresh_token` grant | Z9L3ANetu162tx7jRj9xMmQWkjFBsVu4EAqjtxbt

> Example response

```json
{
  "access_token": "S0kB3MNIF5ZKzOZn4sw8sneKOp71tsynfD2zAUqa",
  "token_type": "Bearer",
  "expires_in": 3600,
  "refresh_token": "Z9L3ANetu162tx7jRj9xMmQWkjFBsVu4EAqjtxbt"
}
```






# Foruminfo



## GET foruminfo

Get forumlist, forumtag, and smiley.

### HTTP Request

`GET /foruminfo`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



# Fjb



## Get Banks List

Get bank list

### HTTP Request

`GET /v1/fjb/banks`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Get Kaskus Banks

Get Kaskus bank list

### HTTP Request

`GET /v1/fjb/kaskus_banks`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Get Banks BI List

Get bank BI repository

### HTTP Request

`GET /v1/fjb/bi_banks`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Buy lapak

Buy certain Lapak

### HTTP Request

`POST /v1/fjb/lapak/{lapak_id}/buy_now`

Parameter | Description | Example
--------- | ----------- | ----------- 
lapak_id|Thread ID|566e5f71c721e6b6418b4567

Field | Description | Example
--------- | -----------| -----------
quantity|quantity wanted|3
message|Content of the message|Hello World. This is example of message
address_id|buyer address id|123456789
shipping_agent|shipping agent or method|2
insurance|want to use insurance or no|1 or 0
tips|Tips Brankas|5000



## Approve buy now invoice

Approve specific buy now invoice

### HTTP Request

`POST /v1/fjb/buy_now/{invoice_id}/approval`

Parameter | Description | Example
--------- | ----------- | ----------- 
invoice_id|Offer ID|566e5f71c721e6b6418b4567
mark_as_sold|Mark the offered lapak as sold-out|1
message|Content of the message|Hello World. This is example of message



## Reject buy now invoice

Reject specific buy now invoice

### HTTP Request

`POST /v1/fjb/buy_now/{invoice_id}/rejection`

Parameter | Description | Example
--------- | ----------- | ----------- 
invoice_id|Offer ID|566e5f71c721e6b6418b4567
message|Content of the message|Hello World. This is example of message



## POST fjb/checkouts

Checkout endpoint

### HTTP Request

`POST /v1/fjb/checkouts/{offer_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
offer_id|Offer ID|566e5f71c721e6b6418b4567
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
buyer_name|Recipent name|Hartono Kaskus
buyer_phone|Recipient phone number|081245172123
tips|Tips Brankas|5000
klikbca_id|KlikBCA ID|hartono1234
payment_method|Payment method ID|1



## Get User's Checkout Item

Get user's checkout item sorted by most recent

### HTTP Request

`GET /v1/fjb/checkout_items`

Parameter | Description | Example
--------- | ----------- | ----------- 
cursor|Cursor for next page|eyJvZmZzZXQiOjF9
limit|Number of item per request|10
thread_id|thread_id from lapak|571f3db28ead0e5f000041c6
offer_type|0 for offer nego, 1 for offer buynow|0



## Add new checkout item

Add new item to checkout items 

### HTTP Request

`POST /v1/fjb/checkout_items`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
thread_id|thread_id from lapak that user will buy|5530b28a8ead0e12010041a7
quantity|quantity item that user want to buy|4



## Delete Item from checkout items

Delete item from checkout items by checkout_item_id

### HTTP Request

`DELETE /v1/fjb/checkout_items/{checkout_item_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
checkout_item_id|selected checkout item ID|534b8787efbcff3e188b4675



## Get Checkout Items Count

Get total user's checkout items

### HTTP Request

`GET /v1/fjb/checkout_items/count`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Update checkout item

Update checkout item quantity by checkout_item_id

### HTTP Request

`POST /v1/fjb/checkout_items/{checkout_item_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
checkout_item_id|checkout item ID|5530b28a8ead0e12010041a7
quantity|quantity item that user want to buy|4



## Delete all checkout items user

Delete all items in user checkout items

### HTTP Request

`DELETE /v1/fjb/checkout_items/all`

Parameter | Description | Example
--------- | ----------- | ----------- 



## GET fjb/invoices/feedbacks

Get feedback value by Invoice ID

### HTTP Request

`GET /v1/fjb/invoices/{invoice_id}/feedbacks`

Parameter | Description | Example
--------- | ----------- | ----------- 
invoice_id|Invoice ID|BF6FAA5678A5F77
output|output format (JSON or XML)|json



## POST fjb/invoices/feedbacks

Set feedback value by Invoice ID

### HTTP Request

`POST /v1/fjb/invoices/{invoice_id}/feedbacks`

Parameter | Description | Example
--------- | ----------- | ----------- 
invoice_id|Invoice ID|BF6FAA5678A5F77
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
response|Feedback response|positive | neutral | negative
message|Feedback message|mantap gan



## JB Showcase

Get JB Showcases for home

### HTTP Request

`GET /v1/fjb/showcases`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
forum_ids|Forum ID to provide Recommended For You section (separated by comma)|196,221,283,297



## GET fjb/invoices

Get certain invoice

### HTTP Request

`GET /v1/fjb/invoices/{invoice_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
invoice_id|Invoice ID|BF6FAA5678A5F77
output|output format (JSON or XML)|json



## POST fjb/invoices/transfer_confirmation

Confirm manual transfer

### HTTP Request

`POST /v1/fjb/invoices/{invoice_id}/transfer_confirmation`

Parameter | Description | Example
--------- | ----------- | ----------- 
invoice_id|Invoice ID|BF6FAA5678A5F77
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
name|Origin bank account name|Hartono Kaskus
origin_bank|Origin bank ID|014
account_number|Origin bank account number|35653723782
destination_bank|Destination bank ID|014
date|Transfer date|1453964285
image|Uploaded image URL|http:cdn.kaskusplayground.local/1433143698.jpg



## POST fjb/invoices/shipping_information

Update shipping status

### HTTP Request

`POST /v1/fjb/invoices/{invoice_id}/shipping_information`

Parameter | Description | Example
--------- | ----------- | ----------- 
invoice_id|Invoice ID|BF6FAA5678A5F77
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
shipping_date|Shipping date|1453964285
tracking_number|Shipping Agent's Tracking Number|CGK789127078120931



## POST fjb/invoices/product_confirmation

Confirm product delivery

### HTTP Request

`POST /v1/fjb/invoices/{invoice_id}/product_confirmation`

Parameter | Description | Example
--------- | ----------- | ----------- 
invoice_id|Invoice ID|BF6FAA5678A5F77
output|output format (JSON or XML)|json



## Get Invoice Status List

Get invoice status detail

### HTTP Request

`GET /v1/fjb/invoice_status`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Get Invoice Status

Get invoice status detail

### HTTP Request

`GET /v1/fjb/invoice_status/{status_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
status_id|Invoice Status ID|2



## Get Tips

Get tips

### HTTP Request

`GET /v1/fjb/tips`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## GET fjb/selling_invoices

Get seller's list of invoice

### HTTP Request

`GET /v1/fjb/selling_invoices`

Parameter | Description | Example
--------- | ----------- | ----------- 
cursor|Cursor for next page|eyJvZmZzZXQiOjF9
status|Filter by status ID|2
invoice_id|Search by invoice ID|BF6FAA5678A5F77
output|output format (JSON or XML)|json



## GET fjb/buying_invoices

Get buyer's list of invoice

### HTTP Request

`GET /v1/fjb/buying_invoices`

Parameter | Description | Example
--------- | ----------- | ----------- 
cursor|Cursor for next page|eyJvZmZzZXQiOjF9
status|Filter by status ID|2
invoice_id|Search by thread invoice ID|BF6FAA5678A5F77
output|output format (JSON or XML)|json



## Get Notification List

Get Notification List

### HTTP Request

`GET /v1/fjb/notifications`

Parameter | Description | Example
--------- | ----------- | ----------- 
cursor|Cursor for next page|eyJvZmZzZXQiOjF9
limit|Data count per page|2
action_ids|Notification with action id want to be show|2



## Get Unread Notification Count

Get Unread Notification Count

### HTTP Request

`GET /v1/fjb/notifications/count`

Parameter | Description | Example
--------- | ----------- | ----------- 
action_ids|Notification with action id want to be show, it can be multiple ids separated by commas|2



## Get Unread Notification Summary

Get Unread Notification Summary

### HTTP Request

`GET /v1/fjb/notification/summaries`

Parameter | Description | Example
--------- | ----------- | ----------- 
action_ids|Notification with action id want to be show, it can be multiple ids separated by commas|2



## Mark Notification as Read

Update notification and mark as read

### HTTP Request

`POST /v1/fjb/notifications/{notification_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
notification_id|Notification id|569df0e38ead0ec3000041a7



## Get Offer Detail

Get certain offer

### HTTP Request

`GET /v1/fjb/offers/{offer_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
offer_id|offer mongo id|55efbd2f4d8a4f02d00041a8



## Create new offer

Create new offer for certain Lapak

### HTTP Request

`POST /v1/fjb/lapak/{lapak_id}/offers`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
offer_price|price wanted|35000
quantity|quantity wanted|3
message|Content of the message|Hello World. This is example of message
address_id|buyer address id|123456789
shipping_agent|shipping agent or method|2
insurance|want to use insurance or no|1 or 0



## Approve Offer

Approve specific offer

### HTTP Request

`POST /v1/fjb/offers/{offer_id}/approval`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
shipping_cost|shipping agent price|30000
message|message for buyer|hai boleh juga penawaran agan



## Reject offer

reject specific offer

### HTTP Request

`POST /v1/fjb/offers/{offer_id}/rejection`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
message|message for buyer|hai penawaran agan agak terlalu murah



## GET fjb/offers/seller

Get seller's list of offer

### HTTP Request

`GET /v1/fjb/offers/seller`

Parameter | Description | Example
--------- | ----------- | ----------- 
cursor|Cursor for next page|eyJvZmZzZXQiOjF9
limit|Number of item per request|10
output|output format (JSON or XML)|json



## GET fjb/offers/buyer

Get buyer's list of offer

### HTTP Request

`GET /v1/fjb/offers/buyer`

Parameter | Description | Example
--------- | ----------- | ----------- 
cursor|Cursor for next page|eyJvZmZzZXQiOjF9
limit|Number of item per request|10
output|output format (JSON or XML)|json



## GET fjb/get_oneklik_user_token/{reference_no}

Get BCA Oneklik user token

### HTTP Request

`GET /v1/fjb/get_oneklik_user_token`



## Get Payment Method List

Get payment method list

### HTTP Request

`GET /v1/fjb/payment_methods`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Get Payment Method Detail

Get payment method detail

### HTTP Request

`GET /v1/fjb/payment_methods/{payment_method_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
payment_method_id|Payment method id|2



## Get Provinces

Get province detail

### HTTP Request

`GET /v1/fjb/location/provinces`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Get Province Detail

Get province detail

### HTTP Request

`GET /v1/fjb/location/provinces/{province_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
province_id|Province ID|15



## Get Cities

Get city list

### HTTP Request

`GET /v1/fjb/location/cities`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Get Areas

Get area list

### HTTP Request

`GET /v1/fjb/location/areas`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Get Cities by Province

Get city detail

### HTTP Request

`GET /v1/fjb/location/provinces/{province_id}/cities`

Parameter | Description | Example
--------- | ----------- | ----------- 
province_id|Province ID|15



## Get Areas by City

Get Areas detail

### HTTP Request

`GET /v1/fjb/location/cities/{city_id}/areas`

Parameter | Description | Example
--------- | ----------- | ----------- 
city_id|City ID|35



## Get Shipping Methods List

Get shipping method detail

### HTTP Request

`GET /v1/fjb/shipping_methods`

Parameter | Description | Example
--------- | ----------- | ----------- 
method_id|Shipping Method ID|2



## Get Shipping Methods Detail

Get shipping method list

### HTTP Request

`GET /v1/fjb/shipping_agents/{method_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
method_id|Shipping Method ID|2



## Get Shipping Cost

Get shipping cost detail by thread id

### HTTP Request

`GET /v1/fjb/lapak/{thread_id}/shipping_costs`

Parameter | Description | Example
--------- | ----------- | ----------- 
thread_id|Thread ID|568a4d4d4d8a4f2f1c0041bd
dest_id|Area id of destination (kecamatan)|3862
quantity|Quantity of the offered product|17



## Get City Detail

Get City Detail

### HTTP Request

`GET /v1/fjb/location/cities/{city_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
city_id|City Id|35



## Get Areas Detail

Get Areas Detail (kecamatan)

### HTTP Request

`GET /v1/fjb/location/areas/{area_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
area_id|Areas Id|595



## Get User Saved Addresses

Get logged in user's saved addresses

### HTTP Request

`GET /v1/fjb/location/addresses`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Save New Address

Save new address

### HTTP Request

`POST /v1/fjb/location/addresses`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
province_id|Province ID|15
city_id|City ID|185
area_id|Area ID|2235
title|Address Title|Rumah Mertua
address|Full Address|Jl. Rasuna Said no. 35
owner_name|Address Owner Name|Villia Susanti
owner_phone|Address Owner Phone|08123123123
default|Mark as default|boolean



## Save New Address

Update address

### HTTP Request

`POST /v1/fjb/location/addresses/{address_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
address_id|Address Id|1453889460

Field | Description | Example
--------- | -----------| -----------
province_id|Province Id|15
city_id|City ID|185
area_id|Area ID|2235
title|Address Title|Rumah Mertua
address|Full Address|Jl. Rasuna Said no. 35
owner_name|Address Owner Name|Villia Susanti
owner_phone|Address Owner Phone|08123123123
default|Mark as default|true



## Get Insurance Cost

Get insurance cost

### HTTP Request

`GET /v1/fjb/insurance_cost/{price}/{shipping_method_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
price|Goods Price|100000
shipping_method_id|Shipping Method ID|2



## Get similar lapak

Get similar products to certain lapak

### HTTP Request

`GET /v1/fjb/similar_products/{lapak_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
lapak_id|Lapak Id|568a4d4d4d8a4f2f1c0041bd



## Get Fjb Thread by category

Get Thread List (FJB) of Selected Forum

### HTTP Request

`GET /v1/fjb/{id}/threads`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|forum id|221
output|output format (JSON or XML)|json
page|number of post page|1
limit|limit number of post per page|20
sort|Sorting method (lastpost,thread,postusername,views,replycount,rating,price).|lastpost
order|Ordering method (asc, desc)|desc



## Get Fjb Lapak by category

Get Thread List (Lapak) of Selected Forum

### HTTP Request

`GET /v1/fjb/{id}/lapaks`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|forum id|221
output|output format (JSON or XML)|json
page|number of post page|1
limit|limit number of post per page|20
sort|Sorting method (lastpost,thread).|lastpost
order|Ordering method (asc, desc)|desc
cursor|thread id to get thread after it. Use cursor = 0 to start from beginning|571f4a448ead0e61000041cd



# User



## GET user/feedbacks

Get user's feedbacks

### HTTP Request

`GET /v1/user/{user_id}/feedbacks`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User ID|3
response|Feedback response|positive | neutral | negative
output|output format (JSON or XML)|json



## POST user/wallet

Redeem Money from Celengan to User's Bank Account

### HTTP Request

`POST /v1/user/wallet/redemption`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
amount|User's Desirable Amount to be redeemed|250000
bank_account_id|User's Bank Account ID|1457323795
password|md5 of User's Password|cc689fce639ab2aa69fe308cda19b703



## POST user/wallet

Validate Redeem Request

### HTTP Request

`POST /v1/user/wallet/redemption/validation`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
amount|User's Desirable Amount to be redeemed|250000
bank_account_id|User's Bank Account ID|1457323795
password|md5 of User's Password|cc689fce639ab2aa69fe308cda19b703



## Wallet Summary

Get users balance summary in wallet

### HTTP Request

`GET /v1/user/wallet/summary`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Transactions History

Get users transactions history

### HTTP Request

`GET /v1/user/wallet/transactions`

Parameter | Description | Example
--------- | ----------- | ----------- 



## GET user

Get certain user profile

### HTTP Request

`GET /user/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id|11
output|output format (JSON or XML)|json



## POST user

Update currently logged in user profile

### HTTP Request

`POST /user`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
fullname|User's fullname|Andrew Darwis
address|User's address|Menara Palma
country|User's country|ID
province|User's province|DKI Jakarta
gender|0 for not specified, 1 for MALE, 2 for FEMALE|1
ktp|Nomor Induk Penduduk (KTP)|0000000000000001
day|The number of the day relative to the end of the previous month.                   Values 1 to 28, 29, 30, or 31.|6
month|1 for January, 2 for February, and so on till 12|1
year|The number of the year, may be a two or four digit value, with values between 0-69                   mapping to 2000-2069 and 70-100 to 1970-2000|2014
biography|User's biography|Halo Semua
upload_profile|1 for Upload Profile Picture, -1 for Remove Profile Picture|5



## GET user

Get current user profile

### HTTP Request

`GET /user`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json
include|include extra field|badges



## GET user/visitor

Get certain user's visitor list

### HTTP Request

`GET /user/visitor/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id|11
output|output format (JSON or XML)|json



## GET user/badges

Get certain user's badges list

### HTTP Request

`GET /user/badges/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id|11
output|output format (JSON or XML)|json



## GET user/privacy_setting

Get currently logged in user's privacy setting. Response will be key-value map.           With value (1) means shareable to public, otherwise is (0).

### HTTP Request

`GET /user/privacy_setting`

Parameter | Description | Example
--------- | ----------- | ----------- 
setting|Filter by certain setting|phone
output|output format (JSON or XML)|json



## POST user/privacy_setting

Update privacy settings.

### HTTP Request

`POST /user/privacy_setting`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
gender|Value 1 for shareable, 0 for not|1
email|Value 1 for shareable, 0 for not|1
address|Value 1 for shareable, 0 for not|1
country|Value 1 for shareable, 0 for not|1
province|Value 1 for shareable, 0 for not|1
phone|Value 1 for shareable, 0 for not|1
dateofbirth|Value 1 for shareable, 0 for not|1



## GET user/get_user_option

Get currently logged in user's option.

### HTTP Request

`GET /user/option`

Parameter | Description | Example
--------- | ----------- | ----------- 



## POST user/user_option

Set currently logged in user's option.

### HTTP Request

`POST /user/option`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
push_pm_notification|Pm notification|true/false
push_hot_thread_notification|Hot thread notification|true/false
push_quoted_post_notification|Quoted post notification|true/false
push_friend_request_notification|Friend request notification|true/false
push_thread_replied_notification|Thread replied notification|true/false
push_subscribed_thread_replied_notification|Subscribed thread replied notification|true/false



## POST user/permission

Check currently user permission based on action

### HTTP Request

`POST /v1/user/permissions`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
action|users action permission|see_balance,create_lapak
password|md5(current users password). this is needed if action= see_balance|kaskus



## GET user/forumpermission

Check currently user forum permission

### HTTP Request

`GET /v1/user/forum_permissions`

Parameter | Description | Example
--------- | ----------- | ----------- 



## GET user/fjbpermission

Check currently user FJB permission

### HTTP Request

`GET /v1/user/fjb_permissions`

Parameter | Description | Example
--------- | ----------- | ----------- 



## GET user/latest_visitor

Get certain user's visitor list and profile visit

### HTTP Request

`GET /user/latest_visitor/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id|11
output|output format (JSON or XML)|json



## Resend email verification

Resend Registration Email Verification

### HTTP Request

`POST /v1/user/verification`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
email|user email|kaskuser123[at]gmail[dot]com



## User Registration Verification

Verify the activation code from member.

### HTTP Request

`POST /v1/user/{user_id}/verifications`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|user_id|11

Field | Description | Example
--------- | -----------| -----------
verification_code|40 digit random string|38e8eb6b5871d21f5470b6c5d12a01d56f16f59a



## GET user/user_option

Get currently logged in user's option.

### HTTP Request

`GET /v1/user/options/{category}`

Parameter | Description | Example
--------- | ----------- | ----------- 
category|return specific category only|privacy, push_notification, notification, other



# Wallet



## Get balance history based on last n days

Get users balance history in wallet

### HTTP Request

`GET /v1/user/wallet/balance_chart/{last_n_days}`

Parameter | Description | Example
--------- | ----------- | ----------- 
last_n_days|the number of days to present balance history in wallet (by default is 7)|7
offset_timezone|the number that preset timezone offset|7



# Followed



## GET followed

Get List of followed user

### HTTP Request

`GET /followed`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## POST followed

Follow user

### HTTP Request

`POST /followed/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id|22
output|output format (JSON or XML)|json



## DELETE followed

Delete followed user

### HTTP Request

`DELETE /followed/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id|22
output|output format (JSON or XML)|json



# Follower



## GET follower

Get List of follower user

### HTTP Request

`GET /follower`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



# Forum



## GET forum/top_kaskuser

Return Top Users, Top Moderators, and Top Regional Leaders

### HTTP Request

`GET /forum/top_kaskuser`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## GET forum/events

Return Kaskus Live data and Events Calendar

### HTTP Request

`GET /forum/events`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## GET forum/threads

Get Thread List (forum) of Selected Forum

### HTTP Request

`GET /v1/forum/{id}/threads`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|forum id|21
output|output format (JSON or XML)|json
page|number of post page|1
limit|limit number of post per page|20
sort|Sorting method (lastpost,thread,postusername,views,replycount,rating,price).|lastpost
order|Ordering method (asc, desc)|desc
include|include a spesific field|preview
tags|include a spesific thread with tags delimiter comma|lalalala,terserah



## GET forum/recommendations

Get Recommended forums, thread video, thread image, thread sista

### HTTP Request

`GET /v1/forum/recommendations`

Parameter | Description | Example
--------- | ----------- | ----------- 
forum_ids|Last accessed forum id,maksimum 10 forum ids|20,21,22



## GET forum/showcases

Get Forum Showcases for home

### HTTP Request

`GET /v1/forum/showcases`

Parameter | Description | Example
--------- | ----------- | ----------- 



# Forumlist



## GET forumlist

Get all forum list.

### HTTP Request

`GET /forumlist`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## GET forumlist

Get all subforum list of certain forum.

### HTTP Request

`GET /forumlist/{forum_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
forum_id|forum id|21
output|output format (JSON or XML)|json



# Forumtag



## GET forumtag/all

Return All Tags

### HTTP Request

`GET /forumtag/all`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## GET forumtag/fjb

Return All FJB Tags

### HTTP Request

`GET /forumtag/fjb`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## GET forumtag/list_forum_tag

Return All Forum Tags

### HTTP Request

`GET /forumtag/list_forum_tag`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## GET forumtag/list_forum_subscription

Return All Forum subscription Tags

### HTTP Request

`GET /forumtag/list_forum_subscription`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## GET forumtag/list_navigation_info

Return List navigation info

### HTTP Request

`GET /forumtag/list_navigation_info`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



# Friend



## GET friend

Get List of Currently logged in user's friend.

### HTTP Request

`GET /friend`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## POST friend

Request friend

### HTTP Request

`POST /friend/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id that you want to be friend|11
output|output format (JSON or XML)|json



## DELETE friend

Unfriend user

### HTTP Request

`DELETE /friend/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id that you want to remove|11
output|output format (JSON or XML)|json



## GET friend

Get friendlist of currently logged in user or input userid.

### HTTP Request

`GET /v1/user/{userId}/friends`

Parameter | Description | Example
--------- | ----------- | ----------- 
userId|user id that you want to retrieve the friend list|11
page|number of post page|1
limit|limit number of post per page|10
output|output format (JSON or XML)|json



## DELETE friend

Unfriend user

### HTTP Request

`DELETE /v1/user/friends/{userId}`

Parameter | Description | Example
--------- | ----------- | ----------- 
userId|User id that you want to remove|11
output|output format (JSON or XML)|json



## POST friend

Approve friend request

### HTTP Request

`POST /v1/user/friends/{userId}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id that you want to be friend|11
output|output format (JSON or XML)|json



## POST friend

Create friend request

### HTTP Request

`POST /v1/user/friend/requests/{userId}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id that you want to send friend request|11
output|output format (JSON or XML)|json



# Mutualfriend



## GET mutualfriend

Get List of Mutual friends between currently logged in and user

### HTTP Request

`GET /mutualfriend/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User Id|11
output|output format (JSON or XML)|json



# Mypost



## GET mypost

Get List of User Post

### HTTP Request

`GET /mypost/{user_id}/{thread_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User Id|11
thread_id|Thread Id that you want to see whose post that posted by certain user|2131231231
output|output format (JSON or XML)|json



## GET mypost

Get List of User Post

### HTTP Request

`GET /mypost/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User Id|11
output|output format (JSON or XML)|json



# Myquotedpost



## GET myquotedpost

Get Quoted Post List from logged in user

### HTTP Request

`GET /myquotedpost`

Parameter | Description | Example
--------- | ----------- | ----------- 



# Mythread



## GET mythread

Get List of User Thread

### HTTP Request

`GET /mythread/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User Id|11
output|output format (JSON or XML)|json



# Mywtb



## GET Mywtb/active

Get List of User WTB thread (active)

### HTTP Request

`GET /mywtb/active/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User Id|11
output|output format (JSON or XML)|json



## GET Mywtb/got_it

Get List of User WTB thread (Got It)

### HTTP Request

`GET /mywtb/got_it/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User Id|11
output|output format (JSON or XML)|json



## GET Mywtb

Get List of User WTB thread (Active + Got It)

### HTTP Request

`GET /mywtb/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User Id|11
output|output format (JSON or XML)|json



# Mywts



## GET Mywts/active

Get List of User WTS thread (active)

### HTTP Request

`GET /mywts/active/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User Id|11
output|output format (JSON or XML)|json



## GET Mywts/sold_out

Get List of User WTS thread (Sold Out)

### HTTP Request

`GET /mywts/sold_out/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User Id|11
output|output format (JSON or XML)|json



## GET Mywts

Get List of User WTS thread (Active + Sold out)

### HTTP Request

`GET /mywts/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User Id|11
output|output format (JSON or XML)|json



# Pm



## POST PM

Mark the pm list as read or unread.

### HTTP Request

`POST /pm/{pmIds}`

Parameter | Description | Example
--------- | ----------- | ----------- 
pmIds|pm id you want to mark as, delimited by comma (,)|1964,1967
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
status|status of the pm you want to mark as|'read' or 'unread'



## DELETE PM

Mark the pm list as deleted.

### HTTP Request

`DELETE /pm/{folderId}/{pmIds}`

Parameter | Description | Example
--------- | ----------- | ----------- 
folderId|folder id which pm located|0
pmIds|pm id you want to mark as deleted, delimited by comma (,)|1964,1967
output|output format (JSON or XML)|json



## POST PM

Compose private message.

### HTTP Request

`POST /pm`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
subject|the subject of the private message|subject of the message
message|the message of the private message|the message content
recipient|recipient of the pm delimited by ;|recca;devil



## GET PM

Get pm list from folder id and pm id.

### HTTP Request

`GET /pm/{folderId}/{pmIds}`

Parameter | Description | Example
--------- | ----------- | ----------- 
folderId|folder id which pm located|0
pmIds|pm id you want to mark as deleted, delimited by comma (,)|1964,1967
output|output format (JSON or XML)|json



## POST PM

Move the pm into another folder.

### HTTP Request

`POST /pm/{currentFolderId}/{pmId}`

Parameter | Description | Example
--------- | ----------- | ----------- 
currentFolderId|folder id which pm located|0
pmId|pm id you want to move|1964
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
folder_id|the new folder id destination|0



## GET PM

Get pm list from folder id.

### HTTP Request

`GET /pm/{folderId}`

Parameter | Description | Example
--------- | ----------- | ----------- 
folderId|folder id which pm located|0
output|output format (JSON or XML)|json



# Pmfolder



## GET pmfolder

Get list of Private Message Folder

### HTTP Request

`GET /pmfolder`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## POST pmfolder

Create new private message folder

### HTTP Request

`POST /pmfolder`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
name|Folder name|Folder example



## DELETE pmfolder

Create new private message folder

### HTTP Request

`DELETE /pmfolder/{folder_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
folder_id|Delete private message folder|1234
output|output format (JSON or XML)|json



# Post



## GET post

Get current post detail.

### HTTP Request

`GET /post/{post_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
oauth_callback|Callback url after user do authorization|json



## POST post

Edit current post detail

### HTTP Request

`POST /post/{post_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
post_id|Post that we want to edit|AA21312321321000
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
title|Post title|This is an example of title
message|Content of the post|Hello World. This is example of post
prefix|Prefix for the post (wtb,wts,sold). Only for first post|wts
condition|The condition of the goods. 1 = New, 2 = Second, 4 = Refurbish. Only for first post|1
price|The price of the goods. Only for first post|10000
search_tags|Keyword for searching (for more than 1 use comma separator)|smartphone,mobile.  Only for first post
location|Location of the goods. (1-32)|smartphone,mobile.  Only for first post



## GET post

Similar with /v1/forum_post or /v1/fjb_post or /v1/lapak_post.           It returns post detail regardless of its type. It is a little bit slower than specific post endpoints.

### HTTP Request

`GET /v1/post/{id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|Post Id that we want to get the detail|53454b4754e8ead0e5a38004492
output|output format (JSON or XML)|json
field|post field that need to be filtered|pagetext,text



# Posts



## GET posts

Get post list that contains certain post

### HTTP Request

`GET /posts/{post_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
post_id|Post id|51638f4fa3616e8b55000005
output|output format (JSON or XML)|json



# Reputation



## GET reputation

Get current user's reputation.

### HTTP Request

`GET /reputation`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



## GET reputation

Get reputation for selected post.

### HTTP Request

`GET /reputation/{post_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
post_id|Post id|51638f4fa3616e8b55000005
output|output format (JSON or XML)|json



## POST reputation

Give reputation for selected post

### HTTP Request

`POST /reputation/{post_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
post_id|Post id|51638f4fa3616e8b55000005
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
reputation|Values are (pos) for giving cendol and (neg) for giving bata|pos



# Search



## Search User

Search User.

### HTTP Request

`GET /search/user`

Parameter | Description | Example
--------- | ----------- | ----------- 
q|Username to search|recca
output|output format (JSON or XML)|json



## GET search/forum_recursive

Search Forum Recursively.

### HTTP Request

`GET /search/forum_recursive`

Parameter | Description | Example
--------- | ----------- | ----------- 
q|Query string to search|android
output|output format (JSON or XML)|json
start_date|timestamp|1458532542
end_date|timestamp|1458532542
forum_ids|forum ids, separated by commas|21,22,23
recursive|recursively search to child or not|true



## GET search/classified_recursive

Search Thread / Lapak in FJB Recursively.

### HTTP Request

`GET /search/classified_recursive`

Parameter | Description | Example
--------- | ----------- | ----------- 
q|Query string to search|android
output|output format (JSON or XML)|json
start_date|timestamp|1458532542
end_date|timestamp|1458532542
forum_ids|forum ids, separated by commas|21,22,23
recursive|recursively search to child or not|true



## GET search/forum

Search Forum.

### HTTP Request

`GET /search/forum`

Parameter | Description | Example
--------- | ----------- | ----------- 
q|Query string to search|android
output|output format (JSON or XML)|json
include|valid value: facet|facet
forum_id|Forum ID|8
tags|Multiple tags|musik,Lol
cursor|Cursor for next page|eyJvZmZzZXQiOjEwfQ
page|Number of post page|1
limit|Number of item per request|10



## GET search/classified

Search fjb thread.

### HTTP Request

`GET /search/classified`

Parameter | Description | Example
--------- | ----------- | ----------- 
q|Query with optional filters. Valid filters are 'condition:new,second,refurbish',               'location:province_id1,province_id2', 'fid:forum_id,forum_id2','type:sold,buy,sell',               'price:10' - exact match,'price:10-100' - between,'price:10' - use less than mark,'price:10' -               use greater than mark, 'price:~100' - price between 90 to 110 (about 10%), 'sellerverified:1' - vsl               'donatur:1' - kaskusplus/donatur, 'paymentescrow:1' - menggunakan brankas|android
output|output format (JSON or XML)|json
include|valid value: facet|facet



## GET search/lapak

Search lapak thread.

### HTTP Request

`GET /search/lapak`

Parameter | Description | Example
--------- | ----------- | ----------- 
q|Query with optional filters. Valid filters are 'condition:new,second,refurbish',               'location:province_id1,province_id2', 'fid:forum_id,forum_id2','type:sold,buy,sell','donatur:true',               'price:10' - exact match,'price:10-100' - between,'price:10' - use less than mark,'price:10' - use greater               than mark, 'price:~100' - price between 90 to 110 (about 10%)|android
output|output format (JSON or XML)|json
include|valid value: facet|facet
sort|Sort field: price, date, last_post, title, username, score|desc



## GET search/group

Search Group.

### HTTP Request

`GET /search/group`

Parameter | Description | Example
--------- | ----------- | ----------- 
q|Query string to search|android
output|output format (JSON or XML)|json
include|valid value: facet|facet



## GET search/forum_tags

Search Forum by multiple tags

### HTTP Request

`GET /search/forum_tags`

Parameter | Description | Example
--------- | ----------- | ----------- 
forum_id|Forum ID|8
tags|Multiple tags|musik,Lol
cursor|Cursor for next page|eyJvZmZzZXQiOjEwfQ
page|Number of post page|1
limit|Number of item per request|10



# Stream



## GET stream

Get List of currently logged in's friend and followed users' posts.

### HTTP Request

`GET /stream`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



# Subscribe



## GET subscribe/lapak

Get user subscription list for lapak.

### HTTP Request

`GET /subscribe/lapak`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



# Aws cognito



## Get AWS Cognito Refresh Token

Get AWS Cognito Refresh Token

### HTTP Request

`GET /v1/cognito/tokens`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Upload Image with AWS Cognito

Upload Image with AWS Cognito With Temporary Token

### HTTP Request

`POST /v1/cognito/images`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
key|Temporary Credentials AccessKeyId|ewr34gt34ft3w4gw34f
secret|Temporary Credentials SecretAccessKey|ta4ta34ft436gsryrdtgytyju=09=guy
token|Temporary Credentials SessionToken|4fotup8q34ud34ik96fpu3q48udy84kwjepyjtferydrfj
image|Image want to be uploaded|
image_name|New Image name|kaskus_image_nih_gan
identity_id|Identity Id used to improve security validation|ap-northeast-1:5490ff1e-2cfb-4c4c-9d6a-87059ed9f4ee



# Badge



## Insert badge to userid(s)

Insert badge to userid(s)

### HTTP Request

`POST /v1/badges`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
badge_id|Badge id|1
user_id|single or multiple target user id delimited by ,|11 or 11,36,12



## Delete badge from userid

Delete badge from userid

### HTTP Request

`DELETE /v1/badges/{user_id}/{badge_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
badge_id|Badge id|1
user_id|target user id|11



# Bank accounts



## Get Bank Accounts

Get all of user's bank accounts

### HTTP Request

`GET /v1/user/bank_accounts`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Create new Bank Accounts

Create new Bank Accounts for current logged-in user

### HTTP Request

`POST /v1/user/bank_accounts`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
bank_id|the bank code|111111
name|the bank account name|Christian Bell
account|the bank account number|8830835661
otp|the otp code|456123
password|the logged-in user password (already md5 hashed)|123456789



## Update selected Bank Account

Update selected Bank Account for current logged-in user

### HTTP Request

`POST /v1/user/bank_accounts/{account_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
account_id|selected bank account id|534b8787efbcff3e188b4675

Field | Description | Example
--------- | -----------| -----------
bank_id|the bank code|111111
name|the bank account name|Christian Bell
account|the bank account number|8830835661
otp|the otp code|456123
password|the logged-in user password (already md5 hashed)|123456789



## DELETE selected Bank Account

Update selected Bank Account for current logged-in user

### HTTP Request

`DELETE /v1/user/bank_accounts/{account_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
account_id|selected bank account id|534b8787efbcff3e188b4675



## Validate new Bank Accounts

Validate new Bank Accounts wants to be added

### HTTP Request

`POST /v1/user/bank_accounts/validation`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
bank_id|the bank code|111111
name|the bank account name|Christian Bell
account|the bank account number|8830835661
password|the logged-in user password (already md5 hashed)|123456789



# Content



## GET content/countries

Get Kaskus Countries

### HTTP Request

`GET /v1/content/countries`

Parameter | Description | Example
--------- | ----------- | ----------- 



## GET content/locations

Get Kaskus Location

### HTTP Request

`GET /v1/content/locations`

Parameter | Description | Example
--------- | ----------- | ----------- 



# Categories



## GET categories

Get all categories for FJB.

### HTTP Request

`GET /v1/categories`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



# Fjb_image



## POST fjb_image

Upload image for Lapak or FJB

### HTTP Request

`POST /v1/fjb_image`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
image|image file to be uploaded .jpg, .png, .jpeg, .bmp|
title|image title that will be used as filename|This is an example of title



# Fjb_post



## GET fjb_post

Get fjb post details

### HTTP Request

`GET /v1/fjb_post/{id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|Post Id that we want to get the detail|53454b4754e8ead0e5a38004492
output|output format (JSON or XML)|json
field|post field that need to be filtered|pagetext,text



## POST fjb_post

Create new FJB post

### HTTP Request

`POST /v1/fjb_post`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
thread_id|Thread where post will be created (must be FJB)|54d1e94ec721e61938000050
title|Post title|This is an example of title
message|Content of the post|Hello World. This is example of post



## POST fjb_post

Edit FJB post

### HTTP Request

`POST /v1/fjb_post/{id}/edit`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
title|Post title|This is an example of title
message|Content of the post|Hello World. This is example of post
prefix|Prefix for the post (wtb,wts,sold). Only for first post|wts
condition|The condition of the goods. 1 = New, 2 = Second, 4 = Refurbish. Only for first post|1
price|The price of the goods. Only for first post|10000
search_tags|Keyword for searching (for more than 1 use comma separator)|smartphone,mobile.  Only for first post
location|Location of the goods. (1-32)|smartphone,mobile.  Only for first post



# Fjb_thread



## GET fjb_thread

Read fjb thread based on id. Thread rating can be calculated from vote_total and vote_num.           Rating = vote_total / vote_num.

### HTTP Request

`GET /v1/fjb_thread/{id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|thread id|53145d43a1cb17ab258b4576
output|output format (JSON or XML)|json
page|number of post page|1
limit|limit number of post per page|20
field|post field that need to be filtered|pagetext,text
include|add similar thread|similar
post|get thread by post id|



## GET fjb_thread

Read fjb thread based on id. Thread rating can be calculated from vote_total and vote_num.           Rating = vote_total / vote_num.

### HTTP Request

`GET /v1/fjb_thread/{id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|thread id|53145d43a1cb17ab258b4576
output|output format (JSON or XML)|json
page|number of post page|1
limit|limit number of post per page|20
field|post field that need to be filtered|pagetext,text
include|add similar thread|similar
post|get thread by post id|



## POST fjb_thread

Sundul fjb thread

### HTTP Request

`POST /v1/fjb_thread/{id}/sundul`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|thread id|534b8787efbcff3e188b4675



# Forum_post



## GET forum_post

Get forum post details

### HTTP Request

`GET /v1/forum_post/{id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|Post Id that we want to get the detail|53454b4754e8ead0e5a38004492
output|output format (JSON or XML)|json
field|post field that need to be filtered|pagetext,text
image|show/hide => emoticon, image, bbcode|off



## POST forum_post

Create new forum post

### HTTP Request

`POST /v1/forum_post`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
thread_id|Thread where post will be created (must be forum)|54d1e94ec721e61938000050
title|Post title|This is an example of title
message|Content of the post|Hello World. This is example of post



## POST forum_post

Edit forum post

### HTTP Request

`POST /v1/forum_post/{id}/edit`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
title|Post title|This is an example of title
message|Content of the post|Hello World. This is example of post
meta_images|List of full url of images that we want to set as meta images, with comma as delimiter|http:s.kaskus.id/picture.png,http:s.kaskus.id/picture2.png



# Forum_setting



## GET forum_setting

Get Forum Setting

### HTTP Request

`GET /v1/forum/settings`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json



# Forum_thread



## GET forum_thread

Read forum thread based on id

### HTTP Request

`GET /v1/forum_thread/{id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|thread id|53145d43a1cb17ab258b4576
post|get thread by post id|json
output|output format (JSON or XML)|json
page|number of post page|1
limit|limit number of post per page|20
field|post field that need to be filtered|pagetext,text
image|show/hide => emoticon, image, bbcode|off
night_mode|modify bbcode style|off



## POST forum_thread

Create forum thread based on id

### HTTP Request

`POST /v1/forum_thread`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
forum_id|Forum where thread will be created (must be forum)|21
title|Thread title|This is an example of title
message|Content of the thread (first post)|Hello World. This is example of post



# Friend request



## GET friend request

Get incoming friend request of currently logged in user.

### HTTP Request

`GET /v1/user/friend/requests?type=incoming`

Parameter | Description | Example
--------- | ----------- | ----------- 
page|number of post page|1
limit|limit number of post per page|10
output|output format (JSON or XML)|json



## DELETE friend request

reject incoming friend request 

### HTTP Request

`DELETE /v1/user/friend/requests/{userId}?type=incoming`

Parameter | Description | Example
--------- | ----------- | ----------- 
userId|User id that you want to reject|11
output|output format (JSON or XML)|json



## GET friend request

Get outgoing friend request of currently logged in user.

### HTTP Request

`GET /v1/user/friend/requests?type=outgoing`

Parameter | Description | Example
--------- | ----------- | ----------- 
page|number of post page|1
limit|limit number of post per page|10
output|output format (JSON or XML)|json



## DELETE friend request

cancel outgoing friend request 

### HTTP Request

`DELETE /v1/user/friend/requests/{userId}?type=outgoing`

Parameter | Description | Example
--------- | ----------- | ----------- 
userId|User id that you want to cancel|11
output|output format (JSON or XML)|json



# Hot_thread



## Get Hot Thread Archives

Get List of Hot Thread's Archive

### HTTP Request

`GET /v1/hot_thread_archives`

Parameter | Description | Example
--------- | ----------- | ----------- 
q|Querying hot threads that contains some keywords in title and its first post message|Android
date|Format: YYYY-MM-DD. Querying hot threads that have start date equals with specified date|2015-12-01
output|output format (JSON or XML)|json
include|include a spesific field|preview



## Get Hot Threads

Get List of Current Hot Thread

### HTTP Request

`GET /v1/hot_threads`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json
include|include a spesific field|preview



# Image



## POST image

Upload Image to Amazon S3 without resizing

### HTTP Request

`POST /v1/image/s3`

Parameter | Description | Example
--------- | ----------- | ----------- 
image|image file|



## POST image

Upload Image for Edit Phone Confirmation & Manual Transfer Confirmation

### HTTP Request

`POST /v1/image/{action}`

Parameter | Description | Example
--------- | ----------- | ----------- 
action|image upload purpose|payment_confirmation; id_card; other_id_card
image|image file|



## POST image

Upload Image for Epulsa

### HTTP Request

`POST /v1/image/epulsa/{action}`

Parameter | Description | Example
--------- | ----------- | ----------- 
action|image upload purpose|id_card
image|image file|



## GET image

Upload Image for Edit Phone Confirmation & Manual Transfer Confirmation

### HTTP Request

`GET /v1/image_upload_status/{md5KeyName}`

Parameter | Description | Example
--------- | ----------- | ----------- 
md5KeyName|md5 of image key path|e3a1ad39a080d20e64ae4e6cb7864912



# Lapak



## GET lapak

Read lapak thread based on id. Thread rating can be calculated from vote_total and vote_num.           Rating = vote_total / vote_num.

### HTTP Request

`GET /v1/lapak/{id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|thread id|534b8787efbcff3e188b4675
output|output format (JSON or XML)|json
page|number of post page|1
limit|limit number of post per page|20
field|post field that need to be filtered|pagetext,text
include|add similar thread|similar
post|get thread by post id|



## POST lapak

Create lapak thread

### HTTP Request

`POST /v1/lapak`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
forum_id|Forum where thread will be created (must be FJB)|221
title|Thread title|This is an example of title
message|Content of the thread (first post)|Hello World. This is example of post
prefix|Prefix for the post (wtb,wts,sold). Only for first post|wts
condition|The condition of the goods. The values are 1,2,4. 1 = New, 2 = Second, 4 = Refurbsih.               Only for first post|1
price|The price of the goods. Only for first post|10000
search_tags|Keyword for searching (for more than 1 use comma separator). Only for first post|smartphone,mobile
location|Location of the goods (1-32). Only for first post|24
extra_attributes|Extra attribute for lapak type thread (use JSON string format)|warna:biru,ukuran:besar,kecil (in JSON format with semicolon)
discount|Discount range 0-100|10
pictures|Image for showing off the products / goods. User can upload images up to 5.               So the field should be {Url of picture_1, Url of picture_2, .. Url of picture_5}.               Image should be uploaded in Kaskus CDN.|
payment_mechanism|Selected payment mechanism preferences. 1 is for COD, 2 is for Brankas|[1,2]
shipping_method|Selected shipping method preferences. There are JNE and POS Indonesia|[1,2,3]
address_id|The shipping origin address|1452262652
weight|The weight of the product to be delivered|140
insurance|Shipping method insurance usage preferences|true / false
free_shipping|Free shipping cost|true / false
custom_shipping_method|Other shipping method want to be used|["gojek","PHD"]



## POST lapak

Edit prefix lapak

### HTTP Request

`POST /v1/lapak/{id}/prefix`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|thread id|534b8787efbcff3e188b4675

Field | Description | Example
--------- | -----------| -----------
prefix_id|New Prefix (wtb,wts,sold)|wts



## POST lapak

Sundul lapak thread

### HTTP Request

`POST /v1/lapak/{id}/sundul`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|thread id|534b8787efbcff3e188b4675



# Lapak_post



## GET lapak_post

Get lapak post details

### HTTP Request

`GET /v1/lapak_post/{id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|Post Id that we want to get the detail|53454b4754e8ead0e5a38004492
output|output format (JSON or XML)|json
field|post field that need to be filtered|pagetext,text



## POST lapak_post

Create new lapak post

### HTTP Request

`POST /v1/lapak_post`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
thread_id|Thread where post will be created (must be lapak)|54d1e94ec721e61938000050
title|Post title|This is an example of title
message|Content of the post|Hello World. This is example of post



## POST lapak_post

Edit lapak post

### HTTP Request

`POST /v1/lapak_post/{id}/edit`

Parameter | Description | Example
--------- | ----------- | ----------- 
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
title|Post title|This is an example of title
message|Content of the post|Hello World. This is example of post
prefix|Prefix for the post (wtb,wts,sold). Only for first post|wts
condition|The condition of the goods.               The values are 1,2,4. 1 = New, 2 = Second, 4 = Refurbsih. Only for first post|1
price|The price of the goods. Only for first post|10000
search_tags|Keyword for searching (for more than 1 use comma separator)|smartphone,mobile
location|Location of the goods. (1-32)|24
extra_attributes|Extra attribute for lapak type thread (use JSON string format)|warna:biru,ukuran:besar,kecil (in JSON format with semicolon)
discount|Discount range 0-100|10
pictures|Image for showing off the products / goods. User can upload images up to 5.               So the field should be {Url of picture_1, Url of picture_2, .. Url of picture_5}.               Image should be uploaded in Kaskus CDN.|
payment_mechanism|Selected payment mechanism preferences. 1 is for COD, 2 is for Brankas|[1,2]
shipping_method|Selected shipping method preferences. There are JNE and POS Indonesia|[1,2,3]
address_id|The shipping origin address|1452262652
weight|The weight of the product to be delivered|140
insurance|Shipping method insurance usage preferences|true / false
free_shipping|Free shipping cost|true / false
custom_shipping_method|Other shipping method want to be used|["gojek","PHD"]



# Latest_products



## GET latest_products

get list of latest WTS product from requested only FJB forums.       For each forum we will get five latest items

### HTTP Request

`GET /latest_products`

Parameter | Description | Example
--------- | ----------- | ----------- 
forum_ids|List of forum id separated by comma|210,208
cursor|First request you just to have use cursor:0|0
limit|limit for returned lapak in a request|5
output|output format (JSON or XML)|json



# Otp



## POST otp

Send SMS OTP

### HTTP Request

`POST /v1/otp/{action}`

Parameter | Description | Example
--------- | ----------- | ----------- 
action|Action Name|user

Field | Description | Example
--------- | -----------| -----------
phone|Phone Number|08123456789



# Push notification receiver



## Get Push Notification Receivers

Get push notification receivers

### HTTP Request

`POST /v1/push_notification_blaster`

Parameter | Description | Example
--------- | ----------- | ----------- 
device_type|Device type: apple,android|apple / android
worker|There are currently 4 worker to blast pushnotif|3
application_type|application type: forum,jb|forum



## Get Push Notification Receivers

Get push notification receivers

### HTTP Request

`GET /v1/push_notification_receivers`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|user id|1
application_type|application type: forum,jb|forum



## Get Temporary Push Notification Receivers

Get temporary push notification receivers

### HTTP Request

`GET /v1/temporary_push_notification_receivers`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|user id|1
application_type|application type: forum,jb|forum



# user



## GET v1/user/quoted_posts

Get Quoted Post List from logged in user

### HTTP Request

`GET /v1/user/quoted_posts`

Parameter | Description | Example
--------- | ----------- | ----------- 
page|Number of post page|1
limit|Number of item per request|10



## GET v1/user/subscription/forums

Get user subscription list for forum

### HTTP Request

`GET /v1/user/subscription/forums`

Parameter | Description | Example
--------- | ----------- | ----------- 
cursor|Cursor for next page|eyJvZmZzZXQiOjEwfQ
page|Number of post page|1
limit|Number of item per request|10



## GET v1/user/subscription/fjb_categories

Get user subscription list for fjb categories

### HTTP Request

`GET /v1/user/subscription/fjb_categories`

Parameter | Description | Example
--------- | ----------- | ----------- 
cursor|Cursor for next page|eyJvZmZzZXQiOjEwfQ
page|Number of post page|1
limit|Number of item per request|10



## GET v1/user/subscription/threads

Get user subscription list for threads

### HTTP Request

`GET /v1/user/subscription/threads`

Parameter | Description | Example
--------- | ----------- | ----------- 
page|Number of page|1
limit|Number of item per request|10



## GET v1/user/subscription/videos

Get user subscription list for thread videos

### HTTP Request

`GET /v1/user/subscription/videos`

Parameter | Description | Example
--------- | ----------- | ----------- 
page|Number of page|1
limit|Number of item per request|10



## GET v1/user/subscription/images

Get user subscription list for thread images

### HTTP Request

`GET /v1/user/subscription/images`

Parameter | Description | Example
--------- | ----------- | ----------- 
page|Number of page|1
limit|Number of item per request|10
width|Preferred thumbnail width size|720



# Registration



## Registration Forum

Create a new user

### HTTP Request

`POST /v1/registration/user?service=forum`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
username|unique username|kaskuser123
email|user email address|priasejati[at]sukabola[dot]com
password|encrypted md5 password|cc689fce639ab2aa69fe308cda19b703
gender|0 for FEMALE, 1 for MALE|1
birthdate|users birth date (yyyy-mm-dd)|1987-06-05
fullname|user fullname|Timotius Erick



## Registration

Create a new user

### HTTP Request

`POST /v1/registration/user`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
username|unique username|kaskuser123
email|user email address|priasejati[at]sukabola[dot]com
password|encrypted md5 password|cc689fce639ab2aa69fe308cda19b703
phone|phone number|08123456789
gender|0 for FEMALE, 1 for MALE|1
birthdate|users birth date (yyyy-mm-dd)|1987-06-05
otp|One Time Password received by user via sms|12345678



## Registration Validation

Validate user data in registration process

### HTTP Request

`POST /v1/registration/user/validation`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
username|unique username|kaskuser123
email|user email address|priasejati[at]sukabola[dot]com
phone|phone number|08123456789



# Users



## GET users

Get User by Something

### HTTP Request

`GET /v1/users`

Parameter | Description | Example
--------- | ----------- | ----------- 
username|username to get|recca



# Shipping agent method



## GET Shipping Agent Method

Get user's shipping agent methods

### HTTP Request

`GET /v1/user/shipping_agent_methods`

Parameter | Description | Example
--------- | ----------- | ----------- 



## POST Shipping Agent Method

Add new shipping agent method to user's shipping agent

### HTTP Request

`POST /v1/user/shipping_agent_methods`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
shipping_ids|id for shipping agent method|[1,2,3,4,5]



## DELETE Shipping Agent Method

Delete user's shipping agent methods

### HTTP Request

`DELETE /v1/user/shipping_agent_methods/{id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
ids|id for shipping agent method|1,2,3,4,5



# Smiley



## Get Smiley Categories Legacy

Get smiley groups

### HTTP Request

`GET /v1/smiley_categories`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Get Smiley by category

Get smiley by category Id

### HTTP Request

`GET /v1/smiley/{categoryId}`

Parameter | Description | Example
--------- | ----------- | ----------- 
categoryId|Smiley category id|1



## Get Smiley Categories only for Kaskus Plus

Get smiley kaskus plus

### HTTP Request

`GET /v1/smiley_kaskus_plus`

Parameter | Description | Example
--------- | ----------- | ----------- 



## Get Smiley by category

Get smiley categories and return all of smilies by it's category

### HTTP Request

`GET /v1/smiley/categories/{categoryId}`

Parameter | Description | Example
--------- | ----------- | ----------- 
categoryId|Smiley category id|1



# Sms



## POST sms

Send SMS to specific user_id

### HTTP Request

`POST /v1/sms`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
user_id|Recipient user_id|11
message|Message to be sent|Ntap gan!



# Special_event



## GET special_event

Get Kaskus special event

### HTTP Request

`GET /v1/kaskus/special_events`

Parameter | Description | Example
--------- | ----------- | ----------- 



# Sticker



## Get Sticker by category

Get sticker by category Id

### HTTP Request

`GET /v1/sticker_categories/{categoryId}/stickers`

Parameter | Description | Example
--------- | ----------- | ----------- 
categoryId|Sticker category id|1



# Sticker category



## Get Sticker Category

Get sticker category

### HTTP Request

`GET /v1/sticker_categories`

Parameter | Description | Example
--------- | ----------- | ----------- 



# Thread



## GET thread

Similar with /v1/forum_thread or /v1/fjb_thread or /v1/lapak.       It returns thread detail regardless of its type. It is a little bit slower than specific thread endpoints.

### HTTP Request

`GET /v1/thread/{id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|thread id|53145d43a1cb17ab258b4576
output|output format (JSON or XML)|json
page|number of post page|1
limit|limit number of post per page|20
field|post field that need to be filtered|pagetext,text



## POST thread

Submit rating to thread. User can only rate a thread once       It returns thread detail regardless of its type. It is a little bit slower than specific thread endpoints.

### HTTP Request

`POST /v1/thread/{id}/rate`

Parameter | Description | Example
--------- | ----------- | ----------- 
id|thread id|53145d43a1cb17ab258b4576
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
rate|Rate from 1 to 5|3



## GET thread

Read next or previous forum thread based on forum_id and last post time

### HTTP Request

`GET /v1/thread/{forum_id}/{last_post}/{operation}`

Parameter | Description | Example
--------- | ----------- | ----------- 
forumId|forum where current thread exists|21
lastPostTimestamp|last post time according to thread data|1484574040
operation|direction which thread should be directed to. ENUM('next', 'prev')|next



# Video_preview



## Get Video Preview

Get a youtube video preview

### HTTP Request

`GET /v1/video_previews`

Parameter | Description | Example
--------- | ----------- | ----------- 

Field | Description | Example
--------- | -----------| -----------
encoded_url|Encoded Youtube Video URL|55efbd2f4d8a4fasdasdasfaf02d00041a8



# Vm



## POST vm

Send visitor message to certain user.

### HTTP Request

`POST /vm/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id|11
output|output format (JSON or XML)|json

Field | Description | Example
--------- | -----------| -----------
message|Content of the message|Hello there.. How are you?



## DELETE vm

Delete visitor message to certain user.

### HTTP Request

`DELETE /vm/{vm_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
vm_id|Visitor Message id|11
output|output format (JSON or XML)|json



## GET vm

Get certain user's visitor messages. Pagination works here.

### HTTP Request

`GET /vm/{user_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id|User id|11
output|output format (JSON or XML)|json



## GET vm/conversation

Get certain two users' conversation in visitor messages.

### HTTP Request

`GET /vm/{user_id_1}/{user_id_2}`

Parameter | Description | Example
--------- | ----------- | ----------- 
user_id_1|User id|11
user_id_2|User id|25
output|output format (JSON or XML)|json



# Whoposted



## GET whoposted

Get list of user who reply post in certain thread

### HTTP Request

`GET /whoposted/{thread_id}`

Parameter | Description | Example
--------- | ----------- | ----------- 
thread_id|thread id|5563f7675e8112bced00456d
output|output format (JSON or XML)|json

