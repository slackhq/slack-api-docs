# team_migration_started event

    {
        "type": "team_migration_started",
    }

The `team_migration_started` event is sent when a Slack team is about to be
migrated between servers. **The websocket connection will close immediately after it is sent.**

Occasionally we need to move Slack teams to a new server. To avoid any data
synchronization bugs or race conditions we disconnect all clients from a team
before starting this process. By the time a client has reconnected the process
is usually complete, so the impact is minimal.

When clients receive this event, immediately start a reconnection
process by calling [`rtm.start`](/methods/rtm.start) again. You may
receive occasional `migration_in_progress` errors when re-calling `rtm.start`. If this happens you should wait a few seconds and try again. If the error continues you should wait longer before retrying, and so on.
