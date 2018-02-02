---
title: Renyoo API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='#'>Get the latest Postman collection</a> # must be linked to a GDrive with managed access
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Renyoo API !! If you are here, you know what Renyoo is all about and chances are you've contributed, in whichever capacity, to make it what it is today. Yeah i know the negative connations .. that is intentional :).

So without much ado, lets do what you intend to do here. The UI is pretty self-explanatory and in this age of Digital Navigation, am pretty sure you will not be lost here.

Browse through the menu or search to find your endpoint of interest. Click on one to read about the endpoint in detail and go through the code examples and sample request/response to understand it better. Reach out to us [here](mailto:developer@renyoo.co) in case you need any further assistance. 

Do visit here often and more importantly, contribute to this documentation regularly and make the world a better place for your fellow devlopers.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

I am not sure if Renyoo uses API keys to allow access to the API. If it is, this section must guide on how to do that. 

In case of using API keys, Renyoo expects the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Root Services

## SER1 - GET

```shell
curl -i 
  -H "Content-Type: application/json" 
  -H "x-rnyoo-client: RnyooAndroid" 
  -k http://android.rnyoo.ws/v1/  
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

This endpoint is to know the server status.

### HTTP Request

`GET http://android.rnyoo.ws/v1/ `

### Query/URL Parameters

NONE

### Data Parameters

NA (as its meant for HTTP verbs other than GET)

### Response Parameters

Description about the keys and their values in the response is explained here.

### Error codes

Description about different error codes in the response and the workflows where they are triggered.


<aside class="success">
Additional info about the endpoint.
</aside>

## SER2 - GET

```shell
curl -i 
  -H "Content-Type: application/json" 
  -H "x-rnyoo-client: RnyooAndroid" 
  -k https://api.rnyoo.ws/v1/update_check
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

This endpoint is to check for Android/iOS app update on the Playstore/Appstore respectively.

<aside class="warning">Understand that this is for deployed apps in Production and you must not use it for your development.</aside>

### HTTP Request

`GET https://api.rnyoo.ws/v1/update_check`

### Query/URL Parameters

NONE

### Data Parameters

NA (as its meant for HTTP verbs other than GET)

### Response Parameters

Description about the keys and their values in the response is explained here.

### Error codes

Description about different error codes in the response and the workflows where they are triggered.


## SER2.a - POST

```shell
curl "http://example.com/api/Posts/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific Post.

### HTTP Request

`DELETE http://example.com/Posts/<ID>`

### Query/URL Parameters

NA

### Data Parameters

Description about the keys and values in the request payload.

### Response Parameters

Description about the keys and their values in the response is explained here.

### Error codes

Description about different error codes in the response and the workflows where they are triggered.


# Utilities

# Users

# Pod/Post

# Interests

# Buddies

# Channels

# Groups

# Geotags
