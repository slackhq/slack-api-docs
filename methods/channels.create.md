This method is used to create a channel.

## Arguments

{ARGS}

## Naming

Channel names can only contain lowercase letters, numbers, hyphens, and underscores, and must be 21 characters or less. We will validate the submitted channel name and modify it to meet the above criteria. When calling this method, we recommend storing the channel's `name` value that is returned in the response.

## Response

If successful, the command returns a [channel object](/types/channel), including state information:


	{
	    "ok": true,
	    "channel": {
			"id": "C024BE91L",
			"name": "fun",
			"created": 1360782804,
			"creator": "U024BE7LH",
			"is_archived": false,
			"is_member": true,
			"is_general": false,
			"last_read": "0000000000.000000",
			"latest": null,
			"unread_count": 0,
			"unread_count_display": 0,
			"members": [ … ],
			"topic": { … },
			"purpose": { … }
		}
	}


## Errors

{ERRORS}

## Warnings

{WARNINGS}
