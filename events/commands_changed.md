# commands_changed event type

	{
		"type": "commands_changed",
		"event_ts" : "1361482916.000004"
	}

The `commands_changed` event is sent to all connections for a team when a
slash command for that team is added, removed or changed.

This functionality is only used by our web client. The other APIs required
to support slash command metadata are currently unstable. Until they are
released other clients should ignore this event.
