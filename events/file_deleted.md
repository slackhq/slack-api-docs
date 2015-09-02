# file_deleted event

	{
		"type": "file_deleted",
		"file_id": "F2147483862",
		"event_ts": "1361482916.000004"
	}

The `file_deleted` event is sent to all connected clients for a team when a
file is deleted. Unlike most file events, the `file` property contains a file
ID and not a full file object.
