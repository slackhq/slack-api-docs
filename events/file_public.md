# file_public event

	{
		"type": "file_public",
		"file": { … },
	}

The `file_public` event is sent when a file is made public. It is sent to all
connected clients for all users that have permission to see the file. The
`file` property is a [file object](/types/file) containing information about
the file.
