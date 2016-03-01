
This method pins an item (file, file comment, channel message, or group message) to a particular channel.
The `channel` argument is required and one of `file`, `file_comment`, or `timestamp` must also be specified.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

After making this call the pin is saved to the database and [a `pin_added` event](/events/pin_added) is broadcast via the [RTM API](/rtm).


## Errors

{ERRORS}

## Warnings

{WARNINGS}
