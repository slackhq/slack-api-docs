# file_comment_added event

	{
		"type": "file_comment_added",
		"file": { … },
		"comment": { … }
	}

The `file_comment_added` event is sent when a comment is added to file. It is
sent to all connected clients for users who can see the file. Clients can use
this notification to show comments in real-time for open files.

The `file` property is a [file object](/types/file).
