# channel\_history\_changed message

	{
		"type": "channel_history_changed",
		"latest": "1358877455.000010",
		"ts": "1361482916.000003",
		"event_ts": "1361482916.000004"
	}

A `channel_history_changed` event is sent to all clients in a channel when
bulk changes have occured to that channel's history. When clients receive this
message they should reload chat history for the channel if they have any
cached messages before `latest`.
