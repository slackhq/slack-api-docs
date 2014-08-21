This method is used to leave a channel.

## Arguments

{ARGS}


## Response

	{
	    "ok": true
	}


This method will not return an error if the user was not in the channel before
it was called. Instead the response will include a `not_in_channel` property:

	{
	    "ok": true,
	    "not_in_channel": true
	}


## Errors

{ERRORS}
