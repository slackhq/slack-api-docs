# channel_rename event type

	{
		"type": "channel_rename",
		"channel": {
			"id":"C02ELGNBH",
			"name":"new_name",
			"created":1360782804
		}
	}

The `channel_renamed` event is sent to all connections for a team when a team
channel is renamed. Clients can use this to update their local list of
channels.
