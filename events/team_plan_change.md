# team\_plan_change event type

	{
		"type": "team_plan_change",
		"plan": "std"
	}

The `team_plan_change` event is sent to all connections for a team when a
the current billing plan is changed. Currently possible values are: empty string,
`std`, and `plus`.