# Pawprint JSON serialization

## Pawprint Object

The Pawprint represents a given Pawprint (request shared on `paw.pt`).

*All fields are optional, but a Pawprint must have a least either `paw_request`, `http_request`, or `http_response`.*

```json
{
  "paw_local_uuid":"{SOME UUID STRING}",
  "paw_request":"{ ... see Paw Request Object ... }",
  "http_request":"{SOME HTTP REQUEST}",
  "http_response":"{SOME HTTP RESPONSE}",
}
```

### Local UUID `paw_local_uuid`

Only for Paw. To keep track of which Pawprint requests are created from a given Paw request.

### Paw Request `paw_request`

We probably don't need that yet on Pawprint, but need to store it to be able to import a request back to Paw. See **Paw Request Object**.

### HTTP Request `http_request`

A string that represents the HTTP request shared. e.g.

```http
POST / HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: echo.luckymarmot.com
Connection: close
User-Agent: Paw/2.1 (Macintosh; OS X/10.10.1) GCDHTTPRequest
Content-Length: 90

```

### HTTP Response `http_response`

A string that represents the HTTP response shared. e.g.

```http
HTTP/1.1 200 OK
Server: nginx/1.4.6 (Ubuntu)
Date: Mon, 08 Dec 2014 23:04:51 GMT
Content-Type: text/html; charset=utf-8
Transfer-Encoding: chunked
Connection: close
Access-Control-Allow-Origin: *
Access-Control-Allow-Headers: Content-Type, X-Special-Header

BODY
```

## Paw Request Object

Represents a Paw Request. Here's its structure:

```json
{
  "name":"string",
  "url":"{ATTRIBUTED STRING}",
  "method":"{ATTRIBUTED STRING}",
  "params":[
    {
      "name":"{ATTRIBUTED STRING}",
      "value":"{ATTRIBUTED STRING}",
      "enabled":true
    }
  ],
  "headers":[
    {
      "name":"{ATTRIBUTED STRING}",
      "value":"{ATTRIBUTED STRING}",
      "enabled":true
    }
  ],
  "body":"{ATTRIBUTED STRING}",
  "options":{
    "{OPTION KEY}":"{OPTION_VALUE}"
  }
}
```

### Name `name`

The request name as it should appear on Paw or Pawprint.

### URL `url`

The request URL without query parameters.

### Method `method`

The request method (e.g. `"GET"` or `"POST"`).

### Params `params`

The request query parameters as an array of dictionaries:

* `name`: key of the parameter
* `value`: value of the parameter
* `enabled`: a boolean flag to indicate whether this parameter should be sent

### Headers

The request headers as an array of dictionaries:

* `name`: the header name (e.g. `Content-Type`)
* `value`: the header value  (e.g. `application/json`)
* `enabled`: a boolean flag to indicate whether this header should be sent

### Options

Options should probably not matter for Pawprint, and will be mostly used when importing files back to Paw.

* `timeout`: request timeout in seconds
* `follow_redirections`: whether the request should follow HTTP redirections
* `redirect_authorization`: if redirecting, whether the `Authorization` header should be forwarded
* `redirect_method`: if redirecting, whether the original method should be used in the redirection, or instead use `GET` as mentioned in [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt).
* `send_cookies`: whether the cookies saved should be sent in a `Cookie` header
* `store_cookies`: whether the cookies set by the server in a `Set-Cookie` header should be stored for future requests

## Attributed String Object

Either a pure string:

```json
"string"
```

or a composed attributed string, which is an array of components, each being
either a string or a dictionary like:

```json
{
  "identifier":"{DYNAMIC VALUE IDENTIFIER}",
  "data":{
    "{DATA KEY}":"{DATA VALUE}"
  },
  "evaluated":"{AN EVALUATED VALUE}"
}
```
