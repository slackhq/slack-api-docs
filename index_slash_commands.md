
Slash Commands enable Slack users to interact with external services directly from Slack.

* [What are slash commands?](#what_are_commands_)
* [How do slash commands work?](#how_do_commands_work_)
* [Triggering commands](#triggering_a_command)
* [Responding to commands](#responding_to_a_command)
* [Best Practices](#best_practices)
* [SSL](#ssl)
* [Attaching your custom command to an app](#attaching_your_custom_command_to_an_app) 

## What are commands?

Messages that start with a slash `/` are commands and will behave differently from regular messages. For example, you can use the "topic" command to change your current channel's topic to "Hello!" by typing `/topic Hello!`. When you type `/remind me in 10 minutes to drink a glass of water` the command will set a reminder for you to drink a glass of water in 10 minutes.

Under the hood, there are 3 different kinds of commands. They work similarly, but are useful for different reasons.

### Built-in Commands

Commands like `/topic` and `/remind` are built into Slack, and available to every team. They often work as shortcuts for doing something related to your channel or Slack team quickly from the message input field. [Here's a list](https://slack.zendesk.com/hc/en-us/articles/201259356-Using-slash-commands) of all of the built-in commands and descriptions about what they do. Give them a try!

### Custom Commands

Every team has the ability to create their own custom commands that they can use on their team. For example, you may want to do something very specific like query your employee directory or intranet, or deploy code to your servers. These commands are simple to create for your team and don't have many restrictions.

### App Commands

App commands, like custom commands, have been developed by 3rd parties and trigger an action (like posting a gif, or starting a video conference, or adding something new to your todo list). Because they are intended to be shared with other teams, they are easy to attach to an app and require minimal configuration to install. In order to protect data on teams, app commands also have some additional restrictions:

* They only support HTTP POST requests.
* The external URLs that the command posts message data to must use TLS (https) with a valid certificate. Self-signed certificates are unsupported.
* They inherit the icon and name of the app that they're attached to, and these properties can't be overwritten in the command response message.
* Only users with permission to install apps can add an app to their team. <br/>
_(By default, all users on a Slack team can install apps, but sometimes team owners and admins restrict those privileges to certain users.)_
* On a free team, each app will count as one towards the ten integration limit. <br/>
_(By comparison, custom commands are counted together as one integration on a free team.)_

Since custom commands on your own team have fewer restrictions than app commands, we recommend that developers start by creating a custom command for testing and development and import it to an app when they are ready to release it. [Learn more about building and distributing your own Slack apps](/slack-apps).

## How do commands work?

### Triggering a command

When someone types a custom command or an app command, the message (and its data) will be sent to the configured external URL via `HTTP POST`.  It's up to you, the developer, to do something with the message data and respond back, if desired.

For example, imagine that there's an app command installed called `/weather`. If someone on the example.slack.com team types `/weather 94070` in the #test channel and hits enter, this data would be posted to the external URL: 

	token=gIkuvaNzQIHg97ATvDxqgjtO
	team_id=T0001
	team_domain=example
	channel_id=C2147483705
	channel_name=test
	user_id=U2147483697
	user_name=Steve
	command=/weather
	text=94070
	response_url=https://hooks.slack.com/commands/1234/5678

Typically, this data will be sent to your URL as a HTTP POST with a `content-type` header set as `application/x-www-form-urlencoded`. If you've chosen to have your slash command's URL receive invocations as a GET request, no explicit `content-type` header will be set.

**NOTE:** The URL you provide must be a HTTPS URL with a valid, verifiable SSL certificate. Self-signed certificates cannot be used. [See below](#ssl) for more information.

### Validating the command

When your server receives the above data, you should validate whether to service the request by confirming that the `token` value matches the validation token you received from Slack when creating the command.

![A slash command validation code](/img/api/slash_command_verification_code.png)

Additionally, you can verify whether the `team_id` matches a team that has approved your command for usage.

If the token or team are unknown to your application, you should refuse to service the request and return an error instead.

### Responding to a command

When the external URL receives this data, you have a few different options for how to respond.

If you'd like to just return information in the simplest possible way, it can respond immediately (within 3000 milliseconds) with a plain text string:

	It's 80 degrees right now.

![Default command response - plain text, visible only to user who issued the command](/img/api/cmd_response_default.png)

If you'd like to customize the appearance of the response message with extra [message formatting](https://api.slack.com/docs/formatting) or [attachment fields](https://api.slack.com/docs/attachments), you can respond immediately (within 3000 milliseconds) with a valid JSON payload:

	{
		"text": "It's 80 degrees right now.",
		"attachments": [
			{
				"text":"Partly cloudy today and tomorrow"
			}
		]
	}

Your URL should respond with a HTTP 200 "OK" status code. Any other flavor of response will result in a user-facing error. If you don't want to respond with any message or would rather send your responses later using _delayed responses_, you should still respond to the invocation of your URL with a simple HTTP 200. That said, we strongly recommend that you send some kind of positive affirmation to the user as an ephemeral response, even if it's just a simple confirmation that the command was understood.

**NOTE:** If you are responding with JSON instead of plain text, the `content-type` header of the response must match the disposition of your content, `application/json`.

#### "In Channel" vs "Ephemeral" responses

By default, the response messages sent to commands will only be visible to the user that issued the command (we call these "ephemeral" messages). However, if you would like the response to be visible to all members of the channel in which the user typed the command, you can add a `response_type` of `in_channel` to the JSON response, like this:

	{
		"response_type": "in_channel",
		"text": "It's 80 degrees right now.",
		"attachments": [
			{
				"text":"Partly cloudy today and tomorrow"
			}
		]
	}

When the `response_type` is `in_channel`, **both** the response message and the initial message typed by the user will be shared in the channel. It will look like this:

![Example of a command in channel response](/img/api/cmd_response_in_channel.png)

Setting `response_type` to `ephemeral` is the same as not including the response type at all, and the response message will be visible only to the user that issued the command. For the best clarity of intent, we recommend always declaring your intended `response_type`.

![Example of a command ephemeral response](/img/api/cmd_response_json_ephemeral.png)

#### Delayed responses and multiple responses

If you want to provide additional command response messages, or if you're unable to immediately respond to a command within 3000 milliseconds, use the specific `response_url` we send with our initial execution of your URL to respond to a command at your leisure. With this approach, you can respond to a user commands up to 5 times within 30 minutes of the user's invocation.

Sending HTTP requests to this `response_url` is easy. Just build a JSON POST body in the same format as used when responding to our command invocation request to your registered URL. It supports all of the same fields (`response_type`, `text`, and `attachments`). Then, send that data as an HTTP POST with a `content-type` of `application/json` to the destination specified as the `response_url`.

The only user-facing difference between immediate responses and delayed responses is that "in channel" delayed responses will not include the initial command sent by the user. To echo the command back to the channel, you'll still need to provide a response to Slack's original visit to your invocation URL.

## Best practices

* If you're not ready to respond to an incoming command but still want to acknowledge the user's action by having their slash command displayed within the channel, respond to your URL's invocation with a simplified JSON response containing only the `response_type` field set to `in_channel`: `{"response_type": "in_channel"}`.
* If your command doesn't need to post anything back (either privately or publicly), respond with an empty HTTP 200 response. Best to use this only if the nature of your command makes it obvious that no response is necessary or desired. Even a simple "Got it!" ephemeral response is better than nothing.
* Help your users understand how to use your command. **Provide a help action that explains your command's usage**. If your slash command was `/please`, you should provide a response to `/please help` that lists the other actions available.
* Keep track of the validation token Slack gives you when the command is created. Always validate the `token` field in an incoming slash command request has been issued to you by Slack.

Consult our [Slash Commands Style Guide](https://medium.com/slack-developer-blog/slash-commands-style-guide-4e91272aa43a) for further tips!

## SSL

Slash command URLs must support HTTPS and serve a valid SSL certificate. Self-signed certificates are not allowed. Check out [CloudFlare](https://www.cloudflare.com/ssl/) for an easy way to obtain a valid certificate.

Before submitting a command to your server, Slack will occasionally send your command URLs a simple GET request to verify the certificate. These requests will include a parameter `ssl_check` set to `1`. Mostly, you may ignore these requests, but please do respond with a HTTP 200 OK.

## Attaching your custom command to an app

If you are building a command and want to distribute it to other Slack teams, you'll want to learn all about turning your command into a [Slack app](/slack-apps).

1. Start with a [custom command](https://my.slack.com/services/new/slash-commands) on your own team. Test it on your team and make sure the experience feels right.
2. [Create a new Slack app](http://api.slack.com/applications), or edit an existing one.
3. Import your custom command and make sure it is now accessible via https, so that messages from teams can be sent securely.
4. [Put the Slack Button on your site](https://api.slack.com/docs/slack-button) so that your users can install your app and slash command!
5. When you're ready, [add your app](https://airtable.com/shrBP6blw8I7bOYN0) to the [App Directory](https://slack.com/apps).
