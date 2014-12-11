# team_join event type

	{
		"type": "team_join",
		"user": {
			…
		}
	}

The `team_join` event is sent to all connections for a team when a new team
member joins the team. Clients can use this to update their local cache of
team members.
