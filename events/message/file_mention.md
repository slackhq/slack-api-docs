# file_mention message

	{
		"type": "message",
		"subtype": "file_mention",
		"ts": "1358877455.000010",
		"text": "<@cal> mentioned a file: <https:...7.png|7.png>",
		"file": {...},
		"user": "U2147483697",
	}


A `file_mention` message is sent when a file is mentioned in a channel,
group or direct message.

The `file` property contains a [file objects](/types/file). The `user`
property contains the User ID of the user that mentioned the file (which may
differ from the user that uploaded the file.
