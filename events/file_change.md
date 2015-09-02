# file_change event

	{
		"type": "file_change",
		"file": { … }
	}

The `file_change` event is sent when any property of a file is changed. It is
sent to all connected clients for all users that have permission to see the
file.

The `file` property is a [file object](/types/file) containing information
about the file.
