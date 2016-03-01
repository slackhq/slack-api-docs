OAuth scopes let you specify exactly how your app needs to access a Slack user's account. As an app developer, you specify your desired scopes in the initial [OAuth authorization request](/docs/oauth). When a user is responding to your OAuth request, the requested scopes will be displayed to them when they are asked to approve your request.

![A screen showing the requested scopes during an OAuth request](/img/api/oauth_authorization.png)

## Types of Scopes

Slack uses scopes that refer to the object they grant access to, followed by the class of actions on that object they allow (e.g. `file:write`). Additionally, some scopes have an optional perspective which is either `user`, `bot`, or `admin`, which effects how the action appears in Slack (e.g. `chat:write:user` will send a message from the authorizing user as opposed to your app).

The list of objects includes `files`, `search`, `chat`, and `reactions`, along with many other objects in Slack.
There are currently only three classes of action:

* __read__: Reading the full information about a single resource.
* __write__: Modifying the resource in any way e.g. creating, editing, or deleting.
* __history__: Accessing the message archive of channels, DMs, or private channels.

For example, to request access to the list of channels on a team and the ability to send messages to those channels as a bot, your app would request `channels:read chat:write:bot`.

# OAuth Scopes to API methods

See https://api.slack.com/docs/oauth-scopes#oauth_scopes_to_api_methods for this section.

## Slack app scopes

If you're building a [Slack app](/slack-apps), you will also encounter three other scopes.

* `incoming-webhook` - requesting this scope during the authentication process allows teams to easily install an [incoming webhook](/incoming-webhooks) that can post from your app to a single Slack channel.
* `commands` - similarly, requesting this scope allows teams to install [slash commands](/slash-commands) bundled in your Slack app.
* `bot` - request this scope when your Slack app includes [bot user](/bot-users) functionality. Unlike `incoming-webhook` and `commands`, the `bot` scope grants your bot user access to [a subset of Web API methods](/bot-users#bot-methods).

## Special scopes

Additionally, Slack supports the following special scopes:

* __identify__ : Allows applications to confirm your identity.
* __client__: Allows applications to connect to slack as a client, and post messages on behalf of the user.
* __admin__: Allows applications to perform administrative actions, requires the authed user to be an admin.


### Working with Scopes

When making the initial authorization request, your application can request multiple scopes as a space or comma separated list (e.g. `teams:read users:read`).

    https://slack.com/oauth/authorize?
      client_id=...&
      scope=team%3Aread+users%3Aread

When using the Slack API you can check the HTTP headers to see what OAuth scopes you have, and what the API method accepts.

    $ curl https://slack.com/api/files.list?token=abcd -I
    HTTP/1.1 200 OK
    X-OAuth-Scopes: files:read, chat:write:bot
    X-Accepted-OAuth-Scopes: files:read

`X-OAuth-Scopes` lists the scopes your token has authorized.
`X-Accepted-OAuth-Scopes` lists the scopes that the action checks for.

Please note that **certain scopes cannot be asked for in combination with each other**. For instance, you cannot request both the `bot` scope and the `client` scope. When users arrive at an authorization page requesting invalid scope combinations, they'll see an ugly error stating something to this effect:

    "OAuth error: invalid_scope: Cannot request service scope (bot) with deprecated scopes"


### Deprecated Scopes

The following scopes are deprecated and their use is strongly discouraged:


* __read__: Allows applications to read any messages and state that the user can see.
* __post__: Allows applications to write messages and create content on behalf of the user
