# group_joined event type

	{
		"type": "group_joined",
		"channel": {
			…
		}
	}

The `group_joined` event is sent to all connections for a user when that user
joins a private group. In addition to this message, all existing members of
the group will recieve a [`group_join` message event](/events/messages/group_join).
