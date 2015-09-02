This method is used to join a channel. If the channel does not exist, it is
created.

## Arguments

{ARGS}


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
			"last_read": "1401383885.000061",
			"latest": { … },
			"unread_count": 0,
			"unread_count_display": 0,
			"members": [ … ],
			"topic": {
				"value": "Fun times",
				"creator": "U024BE7LV",
				"last_set": 1369677212
			},
			"purpose": {
				"value": "This channel is for fun",
				"creator": "U024BE7LH",
				"last_set": 1360782804
			}
		}
	}

If you are already in the channel, the response is slightly different.
`already_in_channel` will be true, and a limited `channel` object will be
returned. This allows a client to see that the request to join `GeNERaL` is
the same as the channel `#general` that the user is already in:

	{
	    "ok": true,
	    "already_in_channel": true,
	    "channel": {
	        "id": "C024BE91L",
	        "name": "fun",
	        "created": 1360782804,
	        "creator": "U024BE7LH",
	        "is_archived": false,
	        "is_general": false
	    }
	}


## Errors

{ERRORS}
