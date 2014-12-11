# channel_deleted event type

	{
		"type": "channel_deleted",
		"channel": "C024BE91L"
	}

The `channel_deleted` event is sent to all connections for a team when a team
channel is deleted. Clients can use this to update their local cache of
non-joined channels.
