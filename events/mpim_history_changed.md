# mpim\_history\_changed message

	{
		"type": "mpim_history_changed",
		"latest": "1358877455.000010"
		"ts": "1361482916.000003",
		"event_ts": "1361482916.000004",
		"is_mpim": 1,
	}

A `mpim_history_changed` event is sent to all clients in a mpim when bulk
changes have occured to that mpim's history. When clients receive this
message they should reload chat history for the mpim if they have any cached
messages before `latest`.
