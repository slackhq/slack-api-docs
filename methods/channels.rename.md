This method renames a team channel.

The only people who can rename a channel are team admins, or the person that
originally created the channel. Others will receive a "not_authorized" error.


## Arguments

{ARGS}

## Naming

Channel names can only contain lowercase letters, numbers, hyphens, and underscores, and must be 21 characters or less. We will validate the submitted channel name and modify it to meet the above criteria. When calling this method, we recommend storing the channel's `name` value that is returned in the response.

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

## Warnings

{WARNINGS}
