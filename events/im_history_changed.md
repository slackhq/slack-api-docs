# im\_history\_changed message

	{
		"type": "im_history_changed",
		"latest": "1358877455.000010"
		"ts": "1361482916.000003",
		"event_ts": "1361482916.000004"
	}

A `im_history_changed` event is sent to all clients in a DM channel when
bulk changes have occured to that DM channel's history. When clients recieve
this message they should reload chat history for the channel if they have any
cached messages before `latest`.
