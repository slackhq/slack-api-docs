
This method allows you to exchange a temporary OAuth `code` for an API access token.
This is used as part of the [OAuth authentication flow](/docs/oauth).

As discussed [in RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.3.1) it is possible to supply the Client ID and Client
Secret using the HTTP Basic authentication scheme. If HTTP Basic authentication is used you do not need to supply the
`client_id` and `client_secret` parameters as part of the request.

**Keep your tokens secure**. Do not share tokens with users or anyone else.

## Arguments

{ARGS}


## Response

	{
	    "access_token": "xoxt-23984754863-2348975623103",
	    "scope": "read"
	}

You can use the returned token to call protected API methods on behalf of the user.


# Errors

{ERRORS}

## Warnings

{WARNINGS}
