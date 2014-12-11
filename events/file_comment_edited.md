# file_comment_edited event

	{
		"type": "file_comment_edited",
		"file": { … },
		"comment": { … }
	}

The `file_comment_edited` event is sent when a file comment is edited. It is
sent to all connected clients for users who can see the file. Clients can use
this notification to update comments in real-time for open files.

The `file` property is a [file object](/types/file).
