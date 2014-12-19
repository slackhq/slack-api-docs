# Presence

A user can have one of two possible presence values, `active` or `away`. A user
is active if they have at least one client connected to Slack, and they are not
marked as "away". There are two ways a user can be marked as away: automatic
and manual.

## Automatic Away

The Slack message servers will automatically detect activity based on
messages sent from a client. If they detect no messages in 30 minutes, the
user is marked as automatically away.

However, it's possible to actively use a Slack client without causing any
messages to be sent; in these situations the client can indicate activity has
occured by calling the API. Every Slack API method accepts an additional
`set_active` argument. This can be used to indicate activity has occured while
performing the requested action.

If the user's activity generates no API calls then the client can periodically
call [users.setActive](/methods/users.setActive) to let the Slack servers know
about that activity.

These auto-away rules do not apply to [Bot Users](/bot-users).

## Manual Away

An application can call [users.setPresence](/methods/users.setPresence)
to manually mark a user as `away` or `active`. A manual status set using this
method will persist between connections.

A manual `away` status set using this method overrides the automatic presence
determined by the message server. A manual `active` presence set using this
method indicates that the automatic status should be used instead.
