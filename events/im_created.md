# im_created event type

	{
		"type": "im_created",
		"user": "U024BE7LH",
		"channel": {...}
	}

The `im_created` event is sent to all connections for a user when a new
direct message channel is created that they are a member of.

This message lets the client know that a channel has been created, but the
client should show no changes based on this, just update its internal list of
IM channels. Usually this event is followed by an
[`im_open` event](/events/im_open).

