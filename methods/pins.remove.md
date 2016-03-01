
This method un-pins an item (file, file comment, channel message, or group message) from a channel.
The `channel` argument is required and one of `file`, `file_comment`, or `timestamp` must also be specified.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

After making this call the pin is removed from the database and [a `pin_removed` event](/events/pin_removed) is broadcast via the [RTM API](/rtm).


## Errors

{ERRORS}

## Warnings

{WARNINGS}
