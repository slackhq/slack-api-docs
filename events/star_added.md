# star_added event type

	{
		"type": "star_added",
		"user": "U024BE7LH",
		"item": {
			…
		}
		"event_ts": "1360782804.083113"
	}

When an item is starred, the `star_added` event is sent to all connected
clients for users who can see the content being starred.

See [the `stars.list` method](/methods/stars.list) for details of the
structure of the `item` property.
