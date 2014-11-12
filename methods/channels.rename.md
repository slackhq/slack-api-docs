This method renames a team channel.

The only people who can rename a channel are team admins, or the person that
originally created the channel. Others will recieve a "not_authorized" error.


## Arguments

{ARGS}


## Response


	{
		"ok": true,
		"channel": {
			"id": "C024BE91L",
			"is_channel": true,
			"name": "new_name",
			"created": 1360782804
		}
	}

Returns the channel ID, name and date created (as a unix timestamp).

## Errors

{ERRORS}
