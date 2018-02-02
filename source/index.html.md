---
title: Renyoo API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='#'>Get the latest Postman collection</a> # must be linked to a GDrive with managed access
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

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

Key | Environment | Value
---- | ------ | ------
baseurl | Development | `you-should-know-by-now`
baseurlp | Production | `you-should-know-by-now`
version | NA | `v1`

# Root Services

## SER1 - GET

```shell
curl -i 
  -H "Content-Type: application/json" 
  -H "x-rnyoo-client: RnyooAndroid" 
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
curl -i 
  -H "Content-Type: application/json" 
  -H "x-rnyoo-client: RnyooAndroid" 
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

<aside class="warning">Note that there is no DEV URL availabl. This is used by the deployed apps in Production and you must not use it for your development.</aside>

### HTTP Request

`GET baseurlp/version/update_check`

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
curl -i 
  -H "Content-Type: application/json" 
  -H "x-rnyoo-client: RnyooAndroid" 
  -d '{"android":{"optionalUpdate":{"optionalVersion":"1.0.3","message":"A new version of the application is available, please click below to update to the latest version"},"requiredUpdate":{"minimumVersion":"1.0.3","message":"A new version of the application is available and is required to continue, please click below to update to the latest version"}},"ios":{"optionalUpdate":{"optionalVersion":"1.2","message":"A new version of the app is available."},"requiredUpdate":{"minimumVersion":"1.1","message":"An update is required to continue using this app."}}}'
  -k baseurlp/version/appversions
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint is to set the optional / required app update versions for Android/iOS apps in Playstore/Appstore respectively.

### HTTP Request

`POST baseurlp/version/appversions`

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
curl -i 
  -H "Content-Type: application/json" 
  -H "x-rnyoo-client: RnyooAndroid" 
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

# Users

# Pod/Post

# Interests

# Buddies

# Channels

# Groups

# Geotags
