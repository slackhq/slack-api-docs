# team_profile_change event type

	{
		"type": "team_profile_change",
		"profile": {
			"fields": [
				{
					"id": "Xf06054AAA",
					...
				},
				...
			]
		}
	}

The `team_profile_change` event is sent to all connections for a team when a
team admin updates the field definitions in the team profile. Only the modified
field definitions are included in the payload. Where appropriate, clients should
update to reflect new changes immediately.
