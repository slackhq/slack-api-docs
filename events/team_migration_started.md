# team_migration_started event

	{
		"type": "team_migration_started",
	}

The `team_migration_started` event is sent when a Slack team is about to be
migrated migrated between servers. Immediately after it is sent the websocket
connection will be closed.

Occasionally we need to move Slack teams to a new server. To avoid any data
syncronization bugs or race conditions we disconnect all clients from a team
before starting this process. By the time a client has reconnected the process
is usually complete, so the impact is minimal.

When clients receive this event they can immediately start a reconnection
process by calling [rtm.start](/methods/rtm.start) again. Occasionally you may
receive a `migration_in_progress` error when re-calling rtm.start. If this
happens you should wait a few seconds and try again. If the error continues
you should wait longer before retrying, and so on.
