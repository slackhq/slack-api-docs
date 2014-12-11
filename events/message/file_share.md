# file_share message

	{
		"type": "message",
		"subtype": "file_share",
		"ts": "1358877455.000010",
		"text": "<@cal> uploaded a file: <https:...7.png|7.png>",
		"file": {...},
		"user": "U2147483697",
		"upload": true
	}

A `file_share` message is sent when a file is shared into a channel,
group or direct message.

The `file` property contains a [file objects](/types/file). The `user`
property contains the User ID of the user that shared the file (which may
differ from the user that uploaded the file. The `upload` property
indicates whether this share happened at upload time, or some time later.
