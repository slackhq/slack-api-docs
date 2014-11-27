This method closes a private group.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

If the group was already closed the response will include `no_op` and
`already_closed` properties:


	{
		"ok": true,
		"no_op": true,
		"already_closed": true
	}


## Errors

{ERRORS}


