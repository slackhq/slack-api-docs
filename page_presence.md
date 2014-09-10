# Presence

A user can have one of two possible presence values, `active` or `away`. A user
is active if all of the following are true:

  * They have at least one client currently connected to Slack.
  * They have performed an action in the last 30 minutes.
  * They have not manually set themselves as away (see below).

If any of these conditions are false, the user is away.

The Slack message servers will automatically detect activity based on
messages sent from a client. However, it's possible to actively use a Slack
client without causing any messages to be sent; in these situations the client
should indicate activity has occured by calling the API.

Every Slack API method accepts an additional `set_active` argument. This can
be used to indicate activity has occured while performing the requested
action.

If the user's activity generates no API calls then the client can periodically
call [users.setActive](/methods/users.setActive) to let the Slack servers know
about that activity.

## Manually setting user presence

An application can call [presence.set](/methods/presence.set)
to manually mark a user as `away` or `active`. A manual status set using this
method will persist between connections.

A manual `away` status set using this method overrides the automatic presence
determined by the message server. A manual `active` presence set using this
method indicates that the automatic status should be used instead.
