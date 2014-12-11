# group_join message

	{
		"type": "message",
		"subtype": "group_join",
		"ts": "1358877458.000011",
		"user": "U2147483828",
		"text": "<@U2147483828|cal> has joined the group"
	}

A `group_join` message is sent when a team member joins a private group.

If the user was invited, the message will include an `inviter` property
containing the user ID of the inviting user.
