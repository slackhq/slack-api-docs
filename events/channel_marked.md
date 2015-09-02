# channel_marked event type

	{
		"type": "channel_marked",
		"channel": "C024BE91L",
		"ts": "1401383885.000061"
	}

The `channel_marked` event is sent to all open connections for a user when
that user moves the read cursor in a channel by calling the
[channels.mark API method](/methods/channels.mark).
