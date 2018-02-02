# Headers

<aside class="success">
This section lists down the <code>Request Headers</code> and <code>Response Headers</code> that Renyoo API uses and their possible meaning. Make sure you understand these codes and factor them while interacting with the API.
</aside>

## Request Headers

First few are added explicitly, while the rest are added by the client.

Header  |  Value
---------- | ------- 
content-type | `application/json`
x-rnyoo-client | `RnyooAndroid`
accept | `*/*`
cache-control | `no-cache`
user-agent | `PostmanRuntime/7.1.1`
host | `android.rnyoo.ws`
accept-encoding | `gzip, deflate`

## Response Headers

`HTTP/<VERSION> <HTTP-STATUS-CODE> <MESSAGE>`

e.g.: HTTP/1.1 200 OK	

Header | Notes | Value
-------- | ------- | ------
content-type | -- | `application/json`
vary | -- | `accept`
date | Server current date and time | `Fri, 02 Feb 2018 08:02:16 GMT`
content-length | -- | `141`
access-control-allow-methods | -- | `GET, PUT, POST, DELETE, OPTIONS`
access-control-allow-origin | -- | `*`
access-control-allow-headers | -- | Origin, X-Requested-With, X-Forward-For, Content-Type, Accept, Accept-Encoding, Content-Disposition
server | Server Name | `Rnyoo Aqua-0.1`
X-Rnyoo-Messsage | Message from server for the given Request | `e.g: Let the Bulls run!!`

## Response Body

This section explains the Response body in case of any errors. List of possible error codes can be seen in the next section.

Header | Value | Notes
-------- | ------- | ------
status | `404` | HTTP Status code
error | `Service not found` | Error message
server | `Rnyoo REST API Server` | Server name
serverVersion | `v1.0.0-84-g199a7a3-dirty` | Server version
serverDate | `2018-02-02 08:44:41.710299` | Current date and time on the server
servicesHealth | `true` | `true`OR`false`based on the service availability


