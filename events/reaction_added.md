# reaction_added event type

	{
		"type": "reaction_added",
		"user": "U024BE7LH",
		"name": "thumbsup",
        "item": {
            …
        },
		"event_ts": "1360782804.083113"
	}

When a reaction is added to an item the `reaction_added` event is sent to all connected clients for users who can see the content that was reacted to.

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

