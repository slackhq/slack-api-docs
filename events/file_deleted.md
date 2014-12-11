# file_deleted event

	{
		"type": "file_deleted",
		"file": "F2147483862",
	}

The `file_deleted` event is sent to all connected clients for a team when a
file is deleted. Unlike most file events, the `file` property contains a file
ID and not a full file object.
