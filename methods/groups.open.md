This method opens a private group.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

If the group was already open the response will include `no_op` and
`already_open` properties:


	{
		"ok": true,
		"no_op": true,
		"already_open": true
	}


## Errors

{ERRORS}


