# team_profile_delete event type

	{
		"type": "team_profile_delete",
		"profile": {
			"fields": [
				"Xf06054AAA",
				...
			]
		}
	}

The `team_profile_delete` event is sent to all connections for a team when a
team admin deletes field definitions from the team profile. Only the `id`s of
the deleted field definitions are included in the payload. Where appropriate,
clients should update to reflect new changes immediately.
