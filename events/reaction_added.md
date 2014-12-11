# star_added event type

	{
		"type": "reaction_added",
		"user": "U024BE7LH",
		"name": "thumbsup",
		"item": {
			…
		}
		"event_ts": "1360782804.083113"
	}

When a reaction is added to an item the `reaction_added` event is sent to all connected
clients for users who can see the content that was reacted ti.

See [the `reactions.list` method](/methods/reactions.list) for details of the
structure of the `item` property.
