# team_rename event type

	{
		"type": "team_rename",
		"name": "New Team Name Inc."
	}

The `team_rename` event is sent to all connections for a team when an admin
changes the team name.

Clients can use this to update the display of the team name as soon as it
changes. If they don't the client will recieve the new name the next time it
calls [`rtm.start`](/methods/rtm.start).
