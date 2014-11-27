
This method opens a direct message channel with another member of your Slack team.


## Arguments

{ARGS}


## Response

	{
		"ok": true,
		"channel": {
			"id": "D024BFF1M",
		},
	}

If the channel was already open the response will include `no_op` and
`already_open` properties:


	{
		"ok": true,
		"no_op": true,
		"already_open": true
		"channel": {
			"id": "D024BFF1M",
		},
	}


## Errors

{ERRORS}


