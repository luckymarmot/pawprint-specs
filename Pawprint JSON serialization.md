# Pawprint JSON serialization

## Request Object

Represents a Paw Request. Here's its structure:

```json
{
	"name":"string",
	"local_uuid":"{SOME UUID STRING}",
	"url":"{ATTRIBUTED STRING}",
	"method":"{ATTRIBUTED STRING}",
	"params":[
		{
			"name":"{ATTRIBUTED STRING}",
			"value":"{ATTRIBUTED STRING}",
			"enabled":boolean
		}
	],
	"headers":[
		{
			"name":"{ATTRIBUTED STRING}",
			"value":"{ATTRIBUTED STRING}",
			"enabled":boolean
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

### Local UUID `local_uuid`

Only for Paw. To keep track of which Pawprint requests are created from a given Paw request.

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
