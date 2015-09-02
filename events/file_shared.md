# file_shared event

	{
		"type": "file_shared",
		"file": { … }
	}

The `file_shared` event is sent when a file is shared. It is sent to all
connected clients for all users that have permission to see the file. The
`file` property is a [file object](/types/file) containing information about
the uploaded file.
