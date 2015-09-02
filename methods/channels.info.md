
This method returns information about a team channel.


## Arguments

{ARGS}


## Response

Returns a [channel object](/types/channel):

	{
		"ok": true,
		"channel": {
			"id": "C024BE91L",
			"name": "fun",

			"created": 1360782804,
			"creator": "U024BE7LH",

			"is_archived": false,
			"is_general": false,
			"is_member": true,

			"members": [ … ],

			"topic": { … },
			"purpose": { … },

			"last_read": "1401383885.000061",
			"latest": { … },
			"unread_count": 0,
			"unread_count_display": 0
		}
	}


## Errors

{ERRORS}
