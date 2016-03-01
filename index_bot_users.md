Enable teams to conversationally interact with external services or your custom code by building **bot users**.

<img src="/img/api/guide_bot_user.png" alt="A conversation between @celeste and @officebot" />

# What are bot users?

Bot users have many of the same qualities as their human counterparts: they have profile photos, names, and bios, they exist in the team directory, they can be direct messaged or mentioned, they can post messages and upload files, and they can be invited to and kicked out of channels and private groups.

The biggest difference between bot users and regular users is that instead of interacting with a team via one of Slack's mobile or desktop apps, bot users are controlled programmatically via a bot user token that accesses one or more of Slack's APIs.

Bot users can't "log in," they don't have a password, and they only have access to a [subset](#bot-methods) of all of the API methods available to regular users.

Within a Slack channel, bot users can do nearly anything you can program them to do.

Slack has two different kinds of bot users: custom bots and app bots. Each serves a different purpose and offers different functionality.

## Custom bot users

Every team has the ability to create their own custom bot users that they can use on their team. They do this by going to their team's settings page and [creating a new bot user](https://my.slack.com/services/new/bot).

Custom bot users are useful for when you want to build something custom for your own team, and have no interest in distributing it to other teams.

For example: you may want to do something very specific like send out an HR survey with a special link out to everyone at your company, or a way to listen for mentions of your company's dog mascot and post cute pictures whenever someone mentions his or her name.

## Attaching bot users to a Slack app

If you'd like to [distribute](https://slack.com/apps) your bot user to other Slack teams, then you should attach it to a [Slack app](/slack-apps). This makes it much easier for teams to install via the [Slack Button](/docs/slack-button), lets you control the bot user's icon and name even after it has been installed, and allows you to bundle it with other app functionality like incoming webhooks and slash commands.

Bot users in Slack apps have some [special considerations](#scopes) when using the API.

# What can bot users do?

The primary way bot users interact with people on a given team is by connecting to the [Real Time Messaging API](/rtm) (RTM API for short) and opening up a websocket connection with Slack.

### Monitor and process channel activity

This websocket will send you all of the messages and activity that happen in public and private channels that the bot user is invited to, as well as messages that are sent to it via direct message. A bot user opens this websocket with the RTM API by sending an authenticated call to the `rtm.start` API method. To learn more about connecting to the RTM API, [read the documentation here](/rtm).

### Post messages and react to users
In addition to receiving messages and activity in the channels it belongs to, the RTM API can be used to post messages as well. However, the RTM API only supports posting messages in our [default message formatting](/docs/formatting). It doesn't support attachments or other message formatting modes.

To post more complex messages as a bot user, clients can use the Web API method[`chat.postMessage`](/methods/chat.postMessage). **Be sure and set `as_user` to `true`** and use your bot user token.

The bot user can also use the Web API to [add emoji reactions](/methods/reactions.add) to messages, [upload files](/methods/files.upload), [pin](/methods/pins.add) and [star](/methods/stars.add) messages, and generally behave like any other user on the team.

# Setting up your bot user

After you've figured out what you want your bot user to do and have an idea of how you'll go about implementing it, you'll want to prepare Slack for the arrival of your bot user.

### How do I create custom bot users for my team?
Start by creating a [new bot user
integration](https://my.slack.com/services/new/bot). You'll need to pick a
username for your new bot. Bot usernames can be up to 21 characters long and sorry, you can't name your bot `Slackbot`.

Once you've added the integration to your team, you'll be
granted a [bot access token](/tokens), which you'll use when connecting to our APIs as that bot user.

### How do I distribute my bot user to other teams?
If you are the developer of an app or service that wants to provide bot-based functionality to Slack teams&mdash; or you just are working on something cool you want to share with everyone&mdash; you can **[package your bot user as a Slack app](/slack-apps)** and implement the [Slack button](/docs/slack-button) to make it simple for any team to install.

### Programming bot users
Creating bot users probably means you'll be coding. If you're using an existing library (such as
[node-slack-client](https://github.com/slackhq/node-slack-client)) then your bot access token should be all you need to get started.

If you're writing your own library from scratch, you'll need to write code to
[make authenticated API calls](/web#authentication) and consume
our [Real Time Messaging API](/rtm). After building those basics, you can focus on the interesting functionality of your bot user.

#### Botkit
One easy way to build bot users, especially if you already work with [Node.js](https://nodejs.org), is Howdy's [**Botkit**](http://howdy.ai/botkit/). Botkit is a framework that takes care of most these API gymnastics, so you can focus on your bot's behavior.

### Other differences between bot users and normal users

* **pricing** - Like other APIs and integrations, bot users are free. Unlike regular users, the actions they can perform are somewhat limited. For teams on the Free plan, each bot user counts as a separate integration.

* **account management** - Bot user account management is performed through the integration page for the bot user.

* **presence** - Bot users do not follow the usual rules for automatically being [marked as away when inactive](/docs/presence). In most cases you want a bot user to display as "active" and ready to respond, even if it hasn't posted a message in a while. Use [the users.setPresence API method](/methods/users.setPresence) to set bot users as "away."

### Share your bot user as a Slack app

[Create a Slack app](/slack-apps) to package and distribute your bot user and submit it to our [application directory](https://slack.com/apps).

#### <a name="scopes"></a>Tokens and scopes

When teams add your application and install your bot user, the token belonging to your bot user is imbued with the necessary scopes to use API methods on its own behalf for the team that is installing your bot user.

You may have other OAuth tokens associated with your app or specific users who have authorized it. Those tokens have a time and place, but when you want to use the Web or RTM API as the bot user, you must use the bot access token that has been awarded the `bot` scope. Bot user tokens begin with the characters **`xoxb`**.


#### Retrieving your bot user token

You'll receive team-specific bot tokens as part of the OAuth approval process. Once the team uses the [Slack button](/docs/slack-button) to install your bot user and as you exchange the code for an access token, you'll receive an additional component to the typical access token response:

    {
        "access_token": "xoxp-XXXXXXXX-XXXXXXXX-XXXXX",
        "scope": "incoming-webhook,commands,bot",
        "team_name": "Team Installing Your Hook",
        "team_id": "XXXXXXXXXX",
        "incoming_webhook": {
            "url": "https://hooks.slack.com/TXXXXX/BXXXXX/XXXXXXXXXX",
            "channel": "#channel-it-will-post-to",
            "configuration_url": "https://teamname.slack.com/services/BXXXXX"
        },
        "bot":{
            "bot_user_id":"UTTTTTTTTTTR",
            "bot_access_token":"xoxb-XXXXXXXXXXXX-TTTTTTTTTTTTTT"
        }
    }


The `bot` node of that JSON response contains two fields. `bot_user_id` is the Slack user ID for your bot user on that team. The `bot_access_token` is the OAuth access token you must use when acting on behalf of your bot for that team.

<p class="alert alert_warning"><i class="ts_icon ts_icon_warning"></i> <strong>Secure your bot user tokens</strong>, as with all tokens and credentials. Do not share tokens with users or anyone else. Bot user tokens have particularly expansive capabilities not afforded to typical user tokens issued on behalf of team members.</p>

### API usage

As mentioned above, when you connect to the [Real Time Messaging API](/rtm) or other APIs in the agency of your bot user, you'll need to use your **bot user's** OAuth token, awarded to you when a team authorizes your application.

Bot users can also only call a subset of our API methods. Any method that
cannot be used by a bot user will return a `user_is_bot` error.

Bot users associated with Slack apps are granted access to fewer API methods than those in custom integrations.

If your Slack app needs access to additional methods in the Web API, you'll need to request your [required scopes](/docs/oauth-scopes) separately as part of the authentication flow. Additionally requested scopes are applied to your application tokens but will *not* be applied to your bot user tokens.

The full list of methods that can be used by bot users is:

<a name="bot-methods"></a>

{BOT_METHOD_LIST}

You can tell if a [user object](/types/user) returned by our API is a bot user by checking the `is_bot` property.

