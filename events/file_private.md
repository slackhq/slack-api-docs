# file_private event

	{
		"type": "file_private",
		"file": "F2147483862",
	}

The `file_private` event is sent to all connected clients for a team when a
file is made private. Unlike most file events, the `file` property contains
a file ID and not a full file object.
