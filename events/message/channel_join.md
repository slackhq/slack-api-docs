# channel_join message

	{
		"type": "message",
		"subtype": "channel_join",
		"ts": "1358877458.000011",
		"user": "U2147483828",
		"text": "<@U2147483828|cal> has joined the channel"
	}

A `channel_join` message is sent when a team member joins a channel.

If the user was invited, the message will include an `inviter` property
containing the user ID of the inviting user.
