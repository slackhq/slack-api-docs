This method closes a private channel.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

If the private channel was already closed the response will include `no_op` and
`already_closed` properties:


	{
		"ok": true,
		"no_op": true,
		"already_closed": true
	}


## Errors

{ERRORS}



## Warnings

{WARNINGS}
