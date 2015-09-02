# channel_created event type

	{
		"type": "channel_created",
		"channel": {
			"id": "C024BE91L",
			"name": "fun",
			"created": 1360782804,
			"creator": "U024BE7LH"
		}
	}

The `channel_created` event is sent to all connections for a team when a new
team channel is created. Clients can use this to update their local cache of
non-joined channels.

