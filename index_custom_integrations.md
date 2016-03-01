<img src="/img/api/homepage_custom_integrations-2x.png" class="getting_started_icon" alt="Building custom integrations" />
Use our API's custom tools to build the perfect tailor-made integration for your team. With a few simple methods and some scripting, you can extend Slack to improve your workflow, monitor external services, and coordinate your team's efforts across devices, locations, and functional groups.

Building custom integrations is also a great way to learn what our APIs can do in preparation for building and distributing a [Slack app](/slack-apps) through our [App Directory](https://slack.com/apps).

Here's a short overview of some of the things you can do with the Slack API toolbox.

## Post automated messages to Slack

Our [incoming webhooks](/incoming-webhooks) provide a simple mechanism to send messages into Slack from any service that can post data. Take any output from your external service, do some simple JSON formatting, and send it right into a channel. For example, let's say you have a help ticketing system that you'd like to monitor for new tickets. You can send a very simple message into Slack with a link to the ticket:

	{
		"text": "New Help Ticket Received: http://domain.com/ticket/123456"
	}

Which will display like this:

![Basic incoming webhook message](/img/api/gs_internal_basic_webhook.png)

But you can also provide more context and detail, like the title and text of the new ticket, by using our JSON `attachment` fields.

<pre class="small code_wrap top_margin">{
	"text": "New Help Ticket Received:",
	"attachments": [
		{
			"title": "App hangs on reboot",
			"title_link": "http://domain.com/ticket/123456",
			"text": "If I restart my computer without quitting your app, it stops the reboot sequence.\nhttp://domain.com/ticket/123456",
		}
	]
}</pre>

Which will display like this:

![Incoming webhook message with attachment](/img/api/gs_internal_incoming_webhook.png)

The title is turned into a link using the `title_link` field, and the additional URL in the attachment's `text` field is autolinked by the client app.

Learn more about our [incoming webhooks](/incoming-webhooks), [message formatting](/docs/formatting), and [message attachments](/docs/attachments).

<a href="https://my.slack.com/services/new/incoming-webhook/" class="btn header_btn">Set up an incoming webhook</a>

## Invoke external services with slash commands

[Slash commands](/slash-commands) are messages that begin with a slash character followed by a command and, optionally, some extra info or arguments, like `/weather`. They can be used to invoke an external service straight from Slack: request data from a service, perform calculations, search, or anything else you need them to do.

When a user issues a command, Slack sends a request to a URL you've configured and waits for a response from your service at that URL. The response can simply be text, or you can provide a full JSON payload similar to our incoming webhooks. Additionally, you can choose to respond only to the user that sent the command (what we call an "ephemeral" message), or response messages can be posted in the channel for everyone to see. You can even wait to send feedback to the user and send up to 5 additional response messages as needed.

Continuing with the help ticketing system example, you could make a slash command to quickly show the user a list of open tickets in the system such that only they can see it (so it doesn't fill the channel with noise). Start with a slash command of `/tickets`, and to that add `list`, so the complete command for this use would be `/tickets list`. The script that you send the command to would take that, query the ticket system and return this JSON payload to the slash command:

	{
		"response_type": "ephemeral",
		"text": "Here are the currently open tickets:",
		"attachments": [
			{
				"text": "#123456 http://domain.com/ticket/123456 \n
				#123457 http://domain.com/ticket/123457 \n
				#123458 http://domain.com/ticket/123458 \n
				#123459 http://domain.com/ticket/123459 \n
				#123460 http://domain.com/ticket/123460"
			}
		]
	}

![Ephemeral message from a slash command](/img/api/gs_internal_ephemeral_msg.png)

And if you wanted to retrieve the text of a ticket for discussion within the channel, you could use `/ticket display [ID]` and configure your script to return this payload instead. Note that it's identical to the incoming webhook payload for a new ticket but uses a `response_type` parameter set to `in_channel`.

<pre class="small code_wrap top_margin">{
	"response_type": "in_channel",
	"text": "Ticket #123456: http://domain.com/ticket/123456",
	"attachments": [
		{
			"title": "App hangs on reboot",
			"text": "If I restart my computer without quitting your app, it stops the reboot sequence.",
		}
	]
}</pre>

![In-channel message from a slash command](/img/api/gs_internal_in_channel_msg.png)

Note that in the case of a slash command configured to deliver an `in_channel` response, the message where the user invoked the slash command is sent into the channel. This helps provide context for other users.

Learn more about our [slash commands](/slash-commands), [message formatting](/docs/formatting), and [message attachments](/docs/attachments).

<a href="https://my.slack.com/services/new/slash-commands" class="btn header_btn">Set up a slash command</a>

## Listen for and respond to messages with a bot user

[Bot users](/bot-users) are the Swiss army knife of our integration tools. They connect to our [Real Time Messaging API](/rtm) like human users, which means they can listen to conversations and even call our [Web API](/web), giving them a kind of flexibility that our other DIY tools don't have. Add a bot user to build a conversational interface with any external service.

It's definitely more work than our other integration tools, but the results can be **amazing**.

![Screenshot of a bot discussion](/img/api/guide_bot_user.png)

Learn more about [bot users](/bot-users) and take a look at the [Botkit framework](http://howdy.ai/botkit/) from our friends at [Howdy](http://howdy.ai/).

<a href="https://my.slack.com/services/new/bot" class="btn header_btn">Set up a bot user</a>

## Going further: the Web API

Our [Web API](/web) gives you access to a handy array of [methods](/methods) for interacting directly with your team's data and users. From searching channel history to checking user information to posting messages directly into channels to deleting those messages, this is where the nuts and bolts of integrating with Slack happen.

To get started with the Web API, [create a token](/web) and try the tester functionality on a few of the method pages. The [`chat.postMessage`](/methods/chat.postMessage) and [`channels.history`](/methods/channels.history) methods are both useful and great places to start.



## Going even further: the Real Time Messaging API

The [Real Time Messaging API](/rtm) lets you or your bot user connect directly with our messaging servers to send and receive messages in &mdash; you guessed it &mdash; real time. Having this connection can make interactions between your integration and Slack as fast as you want it to be. We have an [extensive list of events](/events) that are sent through the RTM API for your bot user or other integration to listen for and respond to.

Like bot users, making full use of the RTM API takes a little more effort, but in the long run can produce amazing results.


## Share your integration: turn it into an app

After you have perfected your integration for your team, you can also turn it into a [Slack app](/slack-apps) that every team can install and enjoy.

<a href="/slack-apps" class="btn header_btn">Build a Slack app</a>