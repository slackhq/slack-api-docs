# file_created event

	{
		"type": "file_created",
		"file": { … },
	}

The `file_created` event is sent to all connected clients for a user when that
user uploads a file to Slack. The `file` property is a
[file object](/types/file) containing information about the uploaded file.

When a file is shared with other members of the team (which can happen at
upload time) a [`file_shared` event](/events/file_shared) will also be sent.
