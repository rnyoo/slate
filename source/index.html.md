---
title: Renyoo API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL

toc_footers:
  - <a href='http://conqueringthecommandline.com/book/curl' target='_blank'>Learn more about cURL</a>
  - <a href='#'>Get the latest Postman collection</a> # must be linked to a GDrive with managed access
  - <a href='https://github.com/lord/slate'>Made possible by Slate</a>

includes:
  - headers
  - errors

search: true
---

# Introduction

Welcome to Renyoo API !! If you are here, you know what Renyoo is all about and chances are you've contributed, in whichever capacity, to make it what it is today. Yeah i know the negative connations .. that is intentional :).

So without much ado, lets do what you intend to do here. The UI is pretty self-explanatory and in this age of Digital Navigation, am pretty sure you will not be lost here.

Browse through the menu or search to find your endpoint of interest. Click on one to read about the endpoint in detail and go through the code examples and sample request/response to understand it better. Reach out to us [here](mailto:developer@renyoo.co) in case you need any further assistance. 

Do visit here often and more importantly, contribute to this documentation regularly and make the world a better place for your fellow devlopers.

# Authentication

Renyoo don't use (yet) API keys to allow access to the API for the clients. This is something we wish to do sooner than later but until then, make sure the endpoints are not exposed to others.

<aside class="warning">
This documentation must not be available for everyone except for the devlopers working on Renyoo platform.
</aside>

# Variables

Endpoints aren't exposed to everyone. In case you don't know them, and you have a genuine reason to know, you have to reach us [here](mailto:developer@renyoo.co).

Key | Environment | Value
---- | ------ | ------
baseurl | Development | `you-should-know-by-now`
baseurlp | Production | `you-should-know-by-now`
version | NA | `v1`

# Root Services

## SER1 - GET

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -k baseurl/version/  
```

> The above command returns JSON structured like this:

```json
[
  {
    "server": "Rnyoo REST API Server",
    "serverVersion": "v1.0.0-84-g199a7a3-dirty",
    "serverDate": "2018-02-02 06:37:13.750496",
    "servicesHealth": true
}
]
```

This is the root endpoint to get the Server info and status of the server-side components. 

### HTTP Request

`GET baseurl/version/ `

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

NONE

### Data Parameters

NA 

### Response Parameters

Key | Value | Notes
---- | ------ | ------
server | `Rnyoo REST API Server` | Server name
serverVersion | `v1.0.0-84-g199a7a3-dirty` | Server version
serverDate | `2018-02-02 09:27:41.355367` | Server current date and time
servicesHealth | `true ` | `true`OR`false`based on the service availability

### Error codes

Code | Message | Notes
------ | --------- | --------
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint

<aside class="success">
This must be hit initially and/or subsequently (whenever required) to check if the server is up and show relevant message (alternate workflow) when down.
</aside>

## SER2 - GET

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -k baseurlp/version/update_check
```

> The above command returns JSON structured like this:

```json
{
    "android": {
        "optionalUpdate": {
            "optionalVersion": "1.0.3",
            "message": "A new version of the application is available, please click below to update to the latest version"
        },
        "requiredUpdate": {
            "minimumVersion": "1.0.3",
            "message": "A new version of the application is available and is required to continue, please click below to update to the latest version"
        }
    },
    "ios": {
        "optionalUpdate": {
            "optionalVersion": "1.2",
            "message": "A new version of the app is available."
        },
        "requiredUpdate": {
            "minimumVersion": "1.1",
            "message": "An update is required to continue using this app."
        }
    }
}
```

This endpoint is to check for Android/iOS app minimum/optional version on the Playstore/Appstore respectively.

<aside class="warning">Note that this endpoint uses Production URL. This is used by the deployed apps in Production and you must not use it for your development.</aside>

### HTTP Request

`GET baseurlp/version/update_check`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

NONE

### Data Parameters

NA 

### Response Parameters

Key | Value | Notes
---- | ------ | ------
android | JSON object | Android details
ios | JSON object | iOS details
optionalUpdate | JSON object | optional version details
requiredUpdate | JSON object | required version details
optionalVersion | `1.0.3` | optional update version for the app
minimumVersion | `1.1` | minimum update version for the app
message | `some msg here ` | message to be displayed along with optional / required version suggestion

### Error codes

Code | Message | Notes
------ | --------- | --------
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint

## SER2.a - POST

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -d '{"android":{"optionalUpdate":{"optionalVersion":"1.0.3","message":"A new version of the application is available, please click below to update to the latest version"},"requiredUpdate":{"minimumVersion":"1.0.3","message":"A new version of the application is available and is required to continue, please click below to update to the latest version"}},"ios":{"optionalUpdate":{"optionalVersion":"1.2","message":"A new version of the app is available."},"requiredUpdate":{"minimumVersion":"1.1","message":"An update is required to continue using this app."}}}' \
  -k baseurlp/version/appversions
```

> The above command returns JSON structured like this:

```json
{  
  "This JSON has to be updated" : ":("
}
```

This endpoint is to set the optional / required app update versions, as and when they are available, for Android/iOS apps in Playstore/Appstore respectively.

<aside class="warning">Note that this endpoint uses Production URL. This is used during Production deployment, probably by a CI/CD pipeline and you must not use it for your development.</aside>

### HTTP Request

`POST baseurlp/version/appversions`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

NA

### Data Parameters

Key | Value | Notes
---- | ------ | ------
android | JSON object | Android details
ios | JSON object | iOS details
optionalUpdate | JSON object | optional version details
requiredUpdate | JSON object | required version details
optionalVersion | `1.0.3` | optional update version for the app
minimumVersion | `1.1` | minimum update version for the app
message | `some msg here ` | message to be displayed along with optional / required version suggestion

### Response Parameters

Description about the keys and their values in the response is explained here.

### Error codes

Code | Message | Notes
------ | --------- | --------
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint

## SER3 - GET

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -k baseurl/version/configs
```

> The above command returns JSON structured like this:

```json
{
    "web_domain_url": "https://beta.rnyoo.co",
    "cdn_base_url": "https://rnyoodevusers.s3.amazonaws.com/",
    "fcm_key": "AIzaSyDqFVSPvOjLXQv-1TO1hx9jTXO28kXQqPc"
}
```

This endpoint is to fetch the app configuration.

### HTTP Request

`GET baseurl/version/configs`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

NONE

### Data Parameters

NA

### Response Parameters

Key | Value | Notes
---- | ------ | ------
web_domain_url | `https://beta.rnyoo.co` | explain this
cdn_base_url | `https://rnyoodevusers.s3.amazonaws.com/` | explain this
fcm_key | `AIzaSyDqsmilenowO28kXQqPc` | explain this

### Error codes

Code | Message | Notes
------ | --------- | --------
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint

# Utilities

## SEO1 - GET

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -k baseurl/version/countries
```

> The above command returns JSON structured like this:

```json
[
    {
        "name": "Afghanistan",
        "dial_code": "+93",
        "code": "AF"
    },
    .
    .
    {
        "name": "India",
        "dial_code": "+91",
        "code": "IN"
    },
    .
    .
    {
        "name": "Zimbabwe",
        "dial_code": "+263",
        "code": "ZW"
    }
]
```

This endpoint is to fetch the countries listing.

### HTTP Request

`GET baseurl/version/countries`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

NONE

### Data Parameters

NA

### Response Parameters

Key | Value | Notes
---- | ------ | ------
name | `India` | Country name
dial_code | `+91` | Country calling code
code | `IN` | Country code

### Error codes

Code | Message | Notes
------ | --------- | --------
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint

## SEO2 - GET

```shell
# https://www.epochconverter.com/ to get the value for URL params (t)
curl -i -v -G \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -d 't=1517837468' \
  -k baseurl/version/countries/status
```

> The above command returns JSON structured like this:

```json
[
    {
        "name": "Afghanistan",
        "dial_code": "+93",
        "code": "AF"
    },
    .
    .
    {
        "name": "India",
        "dial_code": "+91",
        "code": "IN"
    },
    .
    .
    {
        "name": "Zimbabwe",
        "dial_code": "+263",
        "code": "ZW"
    }
]
```

This endpoint is to fetch the countries listing (with Timestamp passed as URL param).

### HTTP Request

`GET baseurl/version/countries/status`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

Key | Value | Notes
---- | ------ | ------
t | `1517837468` | UNIX Timestamp

### Data Parameters

NA

### Response Parameters

Key | Value | Notes
---- | ------ | ------
name | `India` | Country name
dial_code | `+91` | Country calling code
code | `IN` | Country code

### Error codes

Code | Message | Notes
------ | --------- | --------
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint


# Users

## SEU0.a - POST

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -d '{"email_s" : "uname@domain.tld"}' \
  -k baseurl/version/users/validate/email 
```

> The above command returns JSON structured like this:

```json
{
    "email_s": "uname@domain.tld",
    "action": "validate",
    "status": "available",
    "message": "You can create Rnyoo account with this email"
}
```

> In case the input email address is already in use by another Renyoo account:

```json
# HTTP Status code will be 400
{
    "email_s":"uname@domain.tld",
    "action":"validate",
    "status":"unavailable",
    "message":"Given email address is already in use by another Rnyoo account"
}
```

This is the endpoint to validate user email availability as part of Account Registration workflow.

### HTTP Request

`POST baseurl/version/users/validate/email`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

NA

### Data Parameters

Key | Value | Notes
------ | ------ | ------
email_s | `uname@domain.tld` | User input email

### Response Parameters

Key | Value | Notes
---- | ------ | ------
email_s | `uname@domain.tld` | --
action | `validate` | --
status | `available` | `available` OR `unavailable`
message | `You can create Rnyoo ... ` | --

### Error codes

Code | Message | Notes
------ | --------- | --------
400 | Bad Request | Email address already in use
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint
500 | Internal server error | Bad POST payload

<aside class="notice">
Make sure that the input email is of valid format before sending the request as the check isn't implemented upstream.
</aside>

## SEU0.b - POST

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -d '{"phoneNumber_s" : "+919030090300"}' \
  -k baseurl/version/users/validate/phonenumber 
```

> The above command returns JSON structured like this:

```json
{
    "phoneNumber_s": "+919030090300",
    "action": "validate",
    "status": "available",
    "message": "You can create Rnyoo account with this email"
}
```

> In case the input phone number is already in use by another Renyoo account:

```json
# HTTP Status code will be 400
{
    "phoneNumber_s":"+919030090300",
    "action":"validate",
    "status":"unavailable",
    "message":"Given phone number is already in use by another Rnyoo account"
}
```

This is the endpoint to validate user phone number availability as part of Account Registration workflow.

### HTTP Request

`POST baseurl/version/users/validate/phonenumber`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

NA

### Data Parameters

Key | Value | Notes
------ | ------ | ------
phoneNumber_s | `+919030090300` | User input phone number

### Response Parameters

Key | Value | Notes
---- | ------ | ------
phoneNumber_s | `+919030090300` | --
action | `validate` | --
status | `available` | `available` OR `unavailable`
message | `You can create Rnyoo ... ` | --

### Error codes

Code | Message | Notes
------ | --------- | --------
400 | Bad Request | Phone number already in use
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint
500 | Internal server error | Bad POST payload

<aside class="notice">
Make sure that the input phone number is of valid format before sending the request as the check isn't implemented upstream.
</aside>

## SEU0.c - POST

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -d '{"screenName_s" : "stallion"}' \
  -k baseurl/version/users/validate/screenname 
```

> The above command returns JSON structured like this:

```json
{
    "screenName_s": "stallion",
    "action": "validate",
    "status": "available",
    "message": "You can create Rnyoo account with this screen name"
}
```

> In case the input screen name is already in use by another Renyoo account:

```json
# HTTP Status code will be 400
{
    "screenName_s":"gekbull",
    "action":"validate",
    "status":"unavailable",
    "message":"Given screen name is already in use by another Rnyoo account"
}
```

This is the endpoint to validate user screen name availability as part of Account Registration workflow.

### HTTP Request

`POST baseurl/version/users/validate/screenname`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

NA

### Data Parameters

Key | Value | Notes
------ | ------ | ------
screenName_s | `stallion` | User input screen name

### Response Parameters

Key | Value | Notes
---- | ------ | ------
screenName_s | `stallion` | --
action | `validate` | --
status | `available` | `available` OR `unavailable`
message | `You can create Rnyoo ... ` | --

### Error codes

Code | Message | Notes
------ | --------- | --------
400 | Bad Request | Screen name already in use
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint
500 | Internal server error | Bad POST payload

<aside class="notice">
Make sure that the input screen name is of valid format before sending the request as the check isn't implemented upstream.
</aside>

## SEU1 - POST

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -d '{"name_t":"Full Name","userType_s":"general", "gender_s":"male", "screenName_s":"stallion","email_s":"uname@domain.tld","phone":{"countryCode":"+91","number":"9030090300"},"platformForReg":"ios","oauthSource":"Google+","timeZone":"GMT +5:30","avatar":"http://rnyooassets.s3.amazonaws.com/avatars/default.png","statusMessage":"I Rnyoo","preferredChannels":["Gadgets"],"devices":{"ios":[{"deviceId":"foobarIOS","registrationId":"foobarIOSRegistrationId","deviceType":"phone","osVersion":"9.1","registeredOn":1527084033}]}, "bio": "Name is Bond."}' \
  -k baseurl/version/users/new 
```

> The above command returns JSON structured like this:

```json
{
    "id": "otwF8kvzsushh0dn6hhMY",
    "action": "new_user",
    "status": "success",
    "activationCode": 481865,
    "activationStatus": false
}
```

> In case the input email address, phone number, screen name is already in use by another Renyoo account:

```json
{
    "action": "new_user",
    "status": "error",
    "reason": "Email, screen name and phone number are already in use"
}
```

This is the endpoint to create user account with Renyoo on Mobile app using Social platform(s).

<aside class="warning">Note that this endpoint is obsolete. Social Registration/Login is a thing of past, aleast for Renyoo..</aside>

### HTTP Request

`POST baseurl/version/users/new`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

NA

### Data Parameters

Key | Value | Notes
------ | ------ | ------
name_t | `Full Name` | letters, numbers, spaces, max20
userType_s | `general` | --
gender_s | `male` | --
screenName_s | `stallion` | unique. letters, numbers, max15
email_s | `uname@domain.tld` | unique. standard format
phone | JSON object hash | 2 keys
countryCode | `+91` | picked up from dropdown
number | `9030090300` | unique. numbers min6 max10
platformForReg | `ios` | `android` OR `ios`
oauthSource | `Google+` | `Google+` OR `Facebook`
timeZone | `GMT +5.30` | --
avatar | `../default.png` | fully qualified address
statusMessage | `I Renyoo` | --
preferredChannels | `["Gadgets"]` | comma separated values in array
devices | JSON object hash | --
ios | JSON object array of hashes w/ 5 keys | `android` OR `ios` based on platformForReg value
deviceId | `foobarIOS` | --
registrationId | `foobarIOSRegistrationId` | --
deviceType | `phone` | --
osVersion | `9.1` | --
registeredOn | `1527084033` | current Unix epoch
bio | `Name is Bond` | --

### Response Parameters

Key | Value | Notes
---- | ------ | ------
id | `otwF8kvzSqndsuAaAJ0dn6hhMY` | `uid` to be passed with subsequent requests.
action | `new_user` | --
status | `success` | `success` OR `error`
activationCode | `481865` | OTP to complete activation
activationStatus | `false` | always `false`
reason | `Reason for failure` | --

### Error codes

Code | Message | Notes
------ | --------- | --------
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint
500 | Internal server error | Bad POST payload

<aside class="notice">
Don't trust the user and make sure user input is validated before hitting the request.
</aside>

## SEU1.a - POST

```shell
# use SHA256 Cryptographic Hash Function on the Password in your respective platforms. Use converters online to test the API.
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -d '{"name_t":"Full Name", "userType_s":"general","gender_s":"female","screenName_s":"stallion","password":"d608joeydontsharefood0786a", "email_s":"uname@domain.tld","phone":{"countryCode":"+91","number":"9030090300"},"platformForReg":"android","oauthSource":"rnyoo","timeZone":"GMT +5:30","avatar":"http://rnyooassets.s3.amazonaws.com/avatars/default.png","statusMessage":"I Rnyoo","preferredChannels":["Gadgets"],"devices":{"android":[{"deviceId":"foobarAndroidNoSocial","registrationId":"foobarAndroidNoSocialRegId","deviceType":"phone","osVersion":"4.1.1","registeredOn":1527084033}]} ,"bio": "I am Italian Stallion!!"}' \
  -k baseurl/version/users/new 
```

> The above command returns JSON structured like this:

```json
{
    "id":"4ROmJvlhvoilakNOg31u1",
    "action":"new_user",
    "status":"success",
    "activationCode":427862,
    "activationStatus":false
}
```

> In case the input email address, phone number, screen name is already in use by another Renyoo account:

```json
{
    "action": "new_user",
    "status": "error",
    "reason": "Email, screen name and phone number are already in use"
}
```

This is the endpoint to create user account with Renyoo on Mobile app.

### HTTP Request

`POST baseurl/version/users/new`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS` OR `RnyooWeb`

### Query/URL Parameters

NA

### Data Parameters

Key | Value | Notes
------ | ------ | ------
name_t | `Full Name` | letters, numbers, spaces, max20
userType_s | `general` | --
gender_s | `male` | --
screenName_s | `stallion` | unique. letters, numbers, max15
email_s | `uname@domain.tld` | unique. standard format
password | `d608joeydontsharefood0786a` | SHA256. min6 1upcase 1number
phone | JSON object hash | 2 keys
countryCode | `+91` | picked up from dropdown
number | `9030090300` | unique. numbers min6 max10
platformForReg | `android` | `android` OR `ios`
oauthSource | `rnyoo` | --
timeZone | `GMT +5.30` | --
avatar | `../default.png` | fully qualified address
statusMessage | `I Renyoo` | --
preferredChannels | `["Gadgets"]` | comma separated values in array
devices | JSON object hash | --
android | JSON object array of hashes w/ 5 keys | `android` OR `ios` based on platformForReg value
deviceId | `foobarAndroidNoSocial` | --
registrationId | `foobarAndroidNoSocialRegId` | --
deviceType | `phone` | --
osVersion | `4.1.1` | --
registeredOn | `1527084033` | current Unix epoch 
bio | `I am Italian Stallion !!` | --

### Response Parameters

Key | Value | Notes
---- | ------ | ------
id | `otwF8kvzSqndsuAaAJ0dn6hhMY` | `uid` to be passed with subsequent requests.
action | `new_user` | --
status | `success` | `success` OR `error`
activationCode | `481865` | OTP to complete activation
activationStatus | `false` | always `false`
reason | `Reason for failure` | --

### Error codes

Code | Message | Notes
------ | --------- | --------
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint
500 | Internal server error | Bad POST payload

<aside class="notice">
Don't trust the user and make sure user input is validated before hitting the request.
</aside>

## SEU1.b - POST

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooWeb" \
  -d '{"name_t":"Full Name","userType_s":"general","gender_s":"male","screenName_s":"stallion","email_s":"uname@domain.tld","phone":{"countryCode":"+91","number":"9030090300"},"platformForReg":"web","oauthSource":"google","timeZone":"GMT +5:30","avatar":"http://rnyooassets.s3.amazonaws.com/avatars/default.png","statusMessage":"I Rnyoo","preferredChannels":["Gadgets"],"devices":{"web":[{"deviceId":"192.168.10.30","registrationId":"foobarRegistrationId", "deviceType":"desktop", "osType":"Windows", "osVersion":"12.0", "browserVersion": "Chrome 36","registeredOn":1414550816}]},"bio": "Name is Bond."}' \
  -k baseurl/version/users/new 
```

> The above command returns JSON structured like this:

```json
{
    "id": "otwF8kvhejdn6hhMY",
    "action": "new_user",
    "status": "success",
    "activationCode": 481865,
    "activationStatus": false
}
```

> In case the input email address, phone number, screen name is already in use by another Renyoo account:

```json
{
    "action": "new_user",
    "status": "error",
    "reason": "Email, screen name and phone number are already in use"
}
```

This is the endpoint to create user account with Renyoo on Web using Social platform(s).

<aside class="warning">Note that this endpoint is obsolete. Social Registration/Login is a thing of past, aleast for Renyoo..</aside>

### HTTP Request

`POST baseurl/version/users/new`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooWeb` | `RnyooWeb`

### Query/URL Parameters

NA

### Data Parameters

Key | Value | Notes
------ | ------ | ------
name_t | `Full Name` | letters, numbers, spaces, max20
userType_s | `general` | --
gender_s | `male` | --
screenName_s | `stallion` | unique. letters, numbers, max15
email_s | `uname@domain.tld` | unique. standard format
phone | JSON object hash | 2 keys
countryCode | `+91` | picked up from dropdown
number | `9030090300` | unique. numbers min6 max10
platformForReg | `web` | --
oauthSource | `google` | `google` OR `facebook`
timeZone | `GMT +5.30` | --
avatar | `../default.png` | fully qualified address
statusMessage | `I Renyoo` | --
preferredChannels | `["Gadgets"]` | comma separated values in array
devices | JSON object hash | --
web | JSON object array of hashes w/ 7 keys | --
deviceId | `192.168.10.30` | --
registrationId | `foobarRegistrationId` | --
deviceType | `desktop` | --
osType | `windows` | --
osVersion | `9.1` | --
browserVersion | `Chrome 36` | --
registeredOn | `1527084033` | current Unix epoch
bio | `Name is Bond` | --

### Response Parameters

Key | Value | Notes
---- | ------ | ------
id | `otwF8kvhornokplease0dhhMY` | `uid` to be passed with subsequent requests.
action | `new_user` | --
status | `success` | `success` OR `error`
activationCode | `481865` | OTP to complete activation
activationStatus | `false` | always `false`
reason | `Reason for failure` | --

### Error codes

Code | Message | Notes
------ | --------- | --------
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint
500 | Internal server error | Bad POST payload

<aside class="notice">
Don't trust the user and make sure user input is validated before hitting the request.
</aside>

## SEU1.c - POST

```shell
# use SHA256 Cryptographic Hash Function on the Password in your respective platforms. Use converters online to test the API.
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooWeb" \
  -d '{"name_t":"Full Name","userType_s":"general","gender_s":"male","screenName_s":"stallion","password":"d608joeydontsharefood0786a","email_s":"uname@domain.tld","phone":{"countryCode":"+91","number":"9030090300"},"platformForReg":"web","oauthSource":"rnyoo","timeZone":"GMT +5:30","avatar":"http://rnyooassets.s3.amazonaws.com/avatars/default.png","statusMessage":"I Rnyoo","preferredChannels":["Gadgets"],"devices":{"web":[{"deviceId":"192.168.0.1","registrationId":"foobarWebRegistrationId","deviceType":"web","osVersion":"4.1.1","registeredOn":1527084033}]},"bio": "I am Italian Stallion"}' \
  -k baseurl/version/users/new 
```

> The above command returns JSON structured like this:

```json
{
    "id":"4ROmJvlholakNOg31u1",
    "action":"new_user",
    "status":"success",
    "activationCode":427862,
    "activationStatus":false
}
```

> In case the input email address, phone number, screen name is already in use by another Renyoo account:

```json
{
    "action": "new_user",
    "status": "error",
    "reason": "Email, screen name and phone number are already in use"
}
```

This is the endpoint to create user account with Renyoo on Web.

### HTTP Request

`POST baseurl/version/users/new`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooWeb` | `RnyooWeb`

### Query/URL Parameters

NA

### Data Parameters

Key | Value | Notes
------ | ------ | ------
name_t | `Full Name` | letters, numbers, spaces, max20
userType_s | `general` | --
gender_s | `male` | --
screenName_s | `stallion` | unique. letters, numbers, max15
email_s | `uname@domain.tld` | unique. standard format
password | `d608joeydontsharefood0786a` | SHA256. min6 1upcase 1number
phone | JSON object hash | 2 keys
countryCode | `+91` | picked up from dropdown
number | `9030090300` | unique. numbers min6 max10
platformForReg | `android` | `android` OR `ios`
oauthSource | `rnyoo` | --
timeZone | `GMT +5.30` | --
avatar | `../default.png` | fully qualified address
statusMessage | `I Renyoo` | --
preferredChannels | `["Gadgets"]` | comma separated values in array
devices | JSON object hash | --
android | JSON object array of hashes w/ 5 keys | `android` OR `ios` based on platformForReg value
deviceId | `foobarAndroidNoSocial` | --
registrationId | `foobarAndroidNoSocialRegId` | --
deviceType | `phone` | --
osVersion | `4.1.1` | --
registeredOn | `1527084033` | current Unix epoch 
bio | `I am Italian Stallion !!` | --

### Response Parameters

Key | Value | Notes
---- | ------ | ------
id | `otwF8kvzSqndsuAaAJ0dn6hhMY` | `uid` to be passed with subsequent requests.
action | `new_user` | --
status | `success` | `success` OR `error`
activationCode | `481865` | OTP to complete activation
activationStatus | `false` | always `false`
reason | `Reason for failure` | --

### Error codes

Code | Message | Notes
------ | --------- | --------
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint
500 | Internal server error | Bad POST payload

<aside class="notice">
Don't trust the user and make sure user input is validated before hitting the request.
</aside>

## SEU2 - POST

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooAndroid" \
  -d '{"uid" : "2JHbBjUEgUhola7x4IfM"}' \
  -k baseurl/version/users/activate 
```

> The above command returns JSON structured like this:

```json
{
    "id": "otwF8kvzholadn6hhMY",
    "action": "activate",
    "status": "success"
}
```

> In case the uid doesn't match:

```json
# status code is 400
{
    "id": "otwF8kvholan6hhMY",
    "action": "activate",
    "status": "error",
    "message": "Unrecognzied / invalid user"
}
```

This is the endpoint to activate user account that is recently registered on Mobile app.

<aside class="notice">
This endpoint must be hit after validating the user input OTP (received on email / mobile) with the one received after successful registration. 
</aside>

### HTTP Request

`POST baseurl/version/users/activate`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooAndroid` | `RnyooAndroid` OR `RnyooiOS`

### Query/URL Parameters

NA

### Data Parameters

Key | Value | Notes
------ | ------ | ------
uid | `222JHbBjholax4IfM` | received during registration

### Response Parameters

Key | Value | Notes
---- | ------ | ------
id | `otwF8kvholan6hhMY` | uid
action | `activate` | --
status | `success` | `success` OR `error`
message | `Reason for failure` | --

### Error codes

Code | Message | Notes
------ | --------- | --------
400 | Bad Request | UID doesn't exist
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint
500 | Internal server error | Bad POST payload

## SEU2.a - POST

```shell
curl -i -v \
  -H "Content-Type: application/json" \
  -H "x-rnyoo-client: RnyooWeb" \
  -d '{"email": "uname@domain.tld", "activationCode": 123123}' \
  -k baseurl/version/users/webactivate 
```

> The above command returns JSON structured like this:

```json
{
    "email": "uname@domain.tld",
    "action": "activate",
    "status": "success"
}
```

> In case the uid doesn't match:

```json
# status code is 400
{
    "email": "uname@domain.tld",
    "action": "activate",
    "status": "error",
    "message": "Not a valid activation code"
}
```

This is the endpoint to activate user account that is recently registered on Web.

<aside class="notice">
This endpoint must be hit with OTP (received on email / mobile) after successful registration. 
</aside>

### HTTP Request

`POST baseurl/version/users/webactivate`

### Request Headers

Key | Value | Notes
---- | ------ | ------
Content-Type | `application/json` | --
x-rnyoo-client | `RnyooWeb` | --

### Query/URL Parameters

NA

### Data Parameters

Key | Value | Notes
------ | ------ | ------
email | `uname@domain.tld` | --
activationCode | `123123` | --

### Response Parameters

Key | Value | Notes
---- | ------ | ------
email | `uname@domain.tld` | --
action | `activate` | --
status | `success` | `success` OR `error`
message | `Reason for failure` | --

### Error codes

Code | Message | Notes
------ | --------- | --------
400 | Bad Request | UID doesn't match / already activated
403 | Access Forbidden | Missing `x-rnyoo-client` header
404 | Service not found | Wrong API endpoint
500 | Internal server error | Bad POST payload


# Pod/Post

# Interests

# Buddies

# Channels

# Groups

# Geotags
