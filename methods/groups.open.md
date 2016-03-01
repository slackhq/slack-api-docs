This method opens a private channel.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

If the private channel was already open the response will include `no_op` and
`already_open` properties:


	{
		"ok": true,
		"no_op": true,
		"already_open": true
	}


## Errors

{ERRORS}



## Warnings

{WARNINGS}
