# file_unshared event

	{
		"type": "file_unshared",
		"file": { … },
	}

The `file_unshared` event is sent when a file is unshared. It is sent to all
connected clients for all users that had permission to see the file. The
`file` property is a [file object](/types/file) containing information about
the unshared file.
