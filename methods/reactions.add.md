
This method adds a reaction (emoji) to an item (file, file comment, channel message, group message, or direct message).
One of `file`, `file_comment`, or the combination of `channel` and `timestamp` must be specified.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

After making this call, the reaction is saved and [a `reaction_added` event](/events/reaction_added) is broadcast through the [RTM API](/rtm) for the calling user.


## Errors

{ERRORS}

## Warnings

{WARNINGS}
