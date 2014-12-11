# channel_joined event type

	{
		"type": "channel_joined",
		"channel": {
			…
		}
	}

The `channel_joined` event is sent to all connections for a user when that
user joins a channel. In addition to this message, all existing members of the
channel will recieve a [`channel_join` message event](/events/messages/channel_join).
