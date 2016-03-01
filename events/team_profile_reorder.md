# team_profile_reorder event type

	{
		"type": "team_profile_reorder",
		"profile": {
			"fields": [
				{
					"id": "Xf06054AAA",
					"ordering": 0,
				},
				...
			]
		}
	}

The `team_profile_reorder` event is sent to all connections for a team when a
team admin reorders the field definitions in the team profile. The payload
includes only the `id` and the `ordering` for each field definition that is
reordered. Where appropriate, clients should update to reflect new changes
immediately.
