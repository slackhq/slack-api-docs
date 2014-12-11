# star_removed event type

	{
		"type": "star_removed",
		"user": "U024BE7LH",
		"item": {
			…
		}
		"event_ts": "1360782804.083113"
	}

When an item is starred the `star_removed` event is sent to all connected
clients for users who can see the content that was starred.

See [the `stars.list` method](/methods/stars.list) for details of the
structure of the `item` property.
