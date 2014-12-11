# team\_pref_change event type

	{
		"type": "team_pref_change",
		"name": "slackbot_responses_only_admins",
		"value": true
	}

The `team_pref_change` event is sent to all connections for a team when a
team preference is changed. Where appropriate clients should update to reflect
new changes immediately.
