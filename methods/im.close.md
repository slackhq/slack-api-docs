
This method closes a direct message channel.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

If the channel was already closed the response will include a `no_op`
property:


	{
		"ok": true,
		"no_op": true,
		"already_closed": true
	}


## Errors

{ERRORS}


