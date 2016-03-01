
This method adds a star to an item (message, file, file comment, channel, private group, or DM) on behalf of the authenticated user.
One of `file`, `file_comment`, `channel`, or the combination of `channel` and `timestamp` must be specified.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

After making this call, the item will be starred and [a `star_added` event](/events/star_added) is broadcast through the [RTM API](/rtm) for the calling user.


## Errors

{ERRORS}

## Warnings

{WARNINGS}
