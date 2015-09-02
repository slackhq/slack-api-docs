
This method removes a reaction (emoji) from an item (file, file comment, channel message, group message, or direct message).
One of `file`, `file_comment`, or the combination of `channel` and `timestamp` must be specified.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

After making this call, the reaction is removed and [a `reaction_removed` event](/events/reaction_removed) is broadcast through the [RTM API](/rtm) for the calling user.


## Errors

{ERRORS}