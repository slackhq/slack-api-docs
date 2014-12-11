# pref_change event type

	{
		"type": "pref_change",
		"name": "messages_theme",
		"value": "dense"
	}

The `pref_change` event is sent to all connections for a user when a user
preference is changed. Clients should update to reflect new changes
immediately.
