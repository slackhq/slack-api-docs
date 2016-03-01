The Slack button is the simplest way to offer your service to teams using Slack.  A Slack button app gives you [incoming webhooks](/incoming-webhooks), [slash commands](/slash-commands) and [bot users](/bot-users) wrapped in OAuth. You write the commands and the webhook that your app needs, and configure the options for your users. With just a few clicks, your users can add your app to their Slack team and start receiving notifications, issuing commands and chatting with your bot.

The Slack button is also a key aspect of sharing your [Slack app](/slack-apps) in our [Application Directory](https://slack.com/apps)!

![Add to Slack](/img/api/add_to_slack_no_config.png)

When someone clicks on the Slack button in your website or app, the [OAuth process](/docs/oauth) begins by asking them to choose their Slack team and account. The app will then configure an incoming webhook, slash commands and/or a bot on their behalf. Users will no longer need to copy and paste HTML, webhook URLs, or API tokens!

![Authorizing a new app](/img/api/add_to_slack_new_app.png)

## Using the Slack button

Here's how to build a Slack app that can be added to any team via the Slack button. It will let your app send messages to Slack (via incoming webhooks), install slash commands and/or add a bot user on their team. From a user experience standpoint, the flow is identical to a normal OAuth 2.0 flow.

### Register your Slack app

Before you do anything else, you'll need to [create your Slack app](/applications/new) to get a `client_id` and `client_secret` to use [with OAuth](/docs/oauth).

<a href="/applications/new" class="btn header_btn">Create your Slack app</a>

### Attach a slash command to your app (optional)

After saving your app, you'll have the option to attach at least one slash command to your app so that teams installing your app will also be able to use your slash commands.

_Note: Slash commands attached to apps must point to URL on your servers with a valid secure certificate._

### Attach a bot user to your app (optional)

After saving your app, you'll have the option to attach a bot user to your app so that teams installing your app will also be able to converse with your bot.

### <a name="button-widget"></a>Add the Slack button

Now you can add the Slack button to your website, ideally in an area that makes sense for users to set up notifications and integrations with other services. Generate the code for your Slack button below:

See https://api.slack.com/docs/slack-button for the button generator.

At this time, the Slack button can request any combination of the `incoming-webhook`,  `bot`, `commands` scopes. The scopes are requested in the `scope` parameter of the Slack button's URL. In addition to these compound scopes, you may also request the specific object scopes you're interested in, like `reactions.read` or `emoji.list`. You can also specify the following three optional parameters:

`redirect_uri` -- The URL to redirect back to upon authorization<br>
`state` -- unique string to be passed back upon completion<br>
`team` -- Slack team ID of the authenticated user to the integration or app to that team

**Note:** the `incoming-webhook` scope is designed to allow you to request permission to post content into the user's Slack team. It intentionally does not include any read privileges, making it perfect for services that want to send posts or notifications into Slack teams that might not want to give read access to messages. For this reason, it cannot be added alongside the `read`, `post`, and `client` scopes.

### Request a token

After someone accepts or denies the OAuth request, Slack redirects them back to your site via the redirect URI (which you passed into the OAuth flow as the `redirect_uri` parameter, or set up when you created the app). If the OAuth request was accepted, the URL will contain a temporary `code` in a GET code parameter, as well as the state you provided in the previous step in a `state` parameter. If the states don't match, the request has been created by a third party and the process should be aborted.

You will need to exchange the `code` for an access token using [the `oauth.access` method](https://api.slack.com/methods/oauth.access). The JSON response from this API call will contain the access token and incoming webhook URL:


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


The `team_name` field will be the name of the team that installed your app, the `channel` will be the channel name that they have chosen to post to, and the `configuration_url` will be the URL that you can point your user to if they'd like to edit or remove this integration in Slack. You can use these fields to personalize the UI on your end to give context about where the incoming webhook will be posting and how they can edit or remove the integration.

If your button is used to install a [bot user](/bot-users), then pay special attention to the `bot` node of the JSON response. It contains `bot_user_id` and `bot_access_token` values, which you will need to use whenever you are acting on behalf of that bot user for that team context. Use the top-level `access_token` value for other integration points.

![Add to Slack configuration](/img/api/add_to_slack_config.png)

You can now start [sending messages via the incoming webhook](/incoming-webhooks), [listening for and responding to slash commands](/slash-commands) and [initiate or respond to conversations with your bot](/bot-users)!

----

### Handling edge cases and errors

Denying authorization: If the user denies your request during the OAuth flow, Slack redirects back to your `redirect_uri` URL with an error parameter.

	http://yourapp.com/oauth?error=access_denied

Revoking authorization: Users can revoke the incoming webhook URL from within Slack. If a user does so, you'll receive an HTTP 404 response with a body of "No service" when you make requests to the incoming webhook URL. If this happens, you should stop posting messages to the that particular incoming webhook URL.

Bot naming error:  Since your bot inherits the name of the app, and is beholden to the same limitations of real user names, your app name can't be over 35 characters if it has a bot user, and it also can't be called "Slackbot".

Email [integrations@slack.com](mailto:integrations@slack.com) with any questions, feedback, or ideas that would help you get more use out of this, and we'll be more than happy to help.

###Share Your Incoming Webhook as a Slack App

[Create a Slack app](/slack-apps) to to package and distribute your incoming webhook and share it in our [application directory](https://slack.com/apps).

