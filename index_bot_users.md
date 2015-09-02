# Bot users

A bot user is a special kind of free user account. They're optimized for
writing bots that connect to Slack using our [Real Time Messaging API](/rtm).

Connecting your bot to Slack in this way allows fine grained control over
which channels your bot is in. You can even invite bots to private groups or
interact with them using direct messages.

Like our other APIs and integrations bot users are free. Unlike regular users
the actions they can perform are limited slightly. For teams on the Free Plan
each bot user counts as a separate integration.

## Getting started

To write a bot, start by creating a [new bot user
integration](https://my.slack.com/services/new/bot). You'll need to pick a
username for your new bot. Then, once the integration is added, you'll be
given an API token.

If you're using an existing library (such as
[node-slack-client](https://github.com/slackhq/node-slack-client)) then this
API token should be all you need to get started.

If you're writing your own library from scratch, you'll need to write code to
[make authenticated API calls](/#basics). Then you can write code to consume
our [Real Time Messaging API](/rtm). And then you can start working on the
interesting functionality of your bot.

## Technical differences between bot users and normal users

In addition to the difference in pricing, there are a few technical
differences between bot users and other Slack accounts.

Bot users do not have a password, so cannot be used to log on to slack.com or
our clients. Account management can be done through the integration page for
the bot user.

Bot users do not follow the [usual rules for automatically being marked as
away when inactive](/docs/presence). In most cases you want a bot to show as
"active" and ready to respond, even if it hasn't posted a message in a while.
If you'd like a bot to show up as "away" you can use [the users.setPresence API
method](methods/users.setPresence).

Bot users can also only call a subset of our API methods. Any method that
cannot be used by a bot user will return a `user_is_bot` error, which will be
documented as an error in the method documentation. The full list of methods
that can be used by bot users is:

{BOT_METHOD_LIST}

You can tell if a [user object](/types/user) returned by our API is a bot by
checking the `is_bot` property.
