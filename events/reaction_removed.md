# reaction_removed event type

	{
		"type": "reaction_removed",
		"user": "U024BE7LH",
		"name": "thumbsup",
		"item": {
			…
		},
		"event_ts": "1360782804.083113"
	}

When a reaction is removed from an item the `reaction_removed` event is sent to all connected clients for users who can see the content that had the reaction.

### Embedded item objects

Embedded `item` nodes are more lightweight than the structures you'll find in [`reactions.list`](/methods/reactions.list).

Here are some examples:

#### Message:

    "item": {
        "type": "message",
        "channel": "C0G9QF9GZ",
        "ts": "1360782400.498405"
    }

#### File:

    "item": {
        "type": "file",
        "file": "F0HS27V1Z"
    }


#### File Comment:

    "item": {
        "type": "file_comment",
        "file_comment": "Fc0HS2KBEZ",
        "file": "F0HS27V1Z"
    }
