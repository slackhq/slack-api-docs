
This method helps you test your calling code.


## Arguments

{ARGS}


## Response

The response includes any supplied arguments:

	{
		"ok": true,
		"args": {
			"foo": "bar"
		}
	}

If called with an `error` argument an error response is returned:

	{
		"ok": false,
		"error": "my_error",
		"args": {
			"error": "my_error"
		}
	}

## Errors

{ERRORS}

## Warnings

{WARNINGS}
