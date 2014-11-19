This method is used to create a channel.

## Arguments

{ARGS}


## Response

If successful, the command returns a [channel object](/types/channel), including state information:


	{
	    "ok": true,
	    "channel": {
			"id": "C024BE91L",
			"name": "fun",
			"created": "1360782804",
			"creator": "U024BE7LH",
			"is_archived": false,
			"is_member": true,
			"is_general": false,
			"last_read": "0000000000.000000",
			"latest": null,
			"unread_count": 0,
			"members": [ … ],
			"topic": { … },
			"purpose": { … }
		},
	}


## Errors

{ERRORS}
