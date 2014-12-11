# presence_change event

	{
		"type": "presence_change",
		"user": "U024BE7LH",
		"presence": "away"
	}

The `presence_change` event is sent to all connections for a team when a
user changes status. Clients can use this to update their local list
of users.

If a user updates their presence manually, the
[`manual_presence_change` event](/events/manual_presence_change) will also be
sent to all connected clients for that user.
