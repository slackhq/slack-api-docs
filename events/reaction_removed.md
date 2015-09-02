# reaction_removed event type

	{
		"type": "reaction_removed",
		"user": "U024BE7LH",
		"name": "thumbsup",
		"item": {
			…
		}
		"event_ts": "1360782804.083113"
	}

When a reaction is removed from an item the `reaction_removed` event is sent to all connected
clients for users who can see the content that had the reaction.

See [the `reactions.list` method](/methods/reactions.list) for details of the
structure of the `item` property.
