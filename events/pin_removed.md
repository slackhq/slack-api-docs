# pin_removed event type

	{
		"type": "pin_removed",
		"user": "U024BE7LH",
		"channel_id": "C02ELGNBH",
		"item": {
			…
		},
		"has_pins": false,
		"event_ts": "1360782804.083113"
	}

When an item is un-pinned from a channel, the `pin_removed` event is sent to all members of that channel.

The `has_pins` property indicates that there are other pinned items in that channel.
