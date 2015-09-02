##Send data into Slack in real-time.

Incoming Webhooks are a simple way to post messages from external sources into Slack. They make use of normal HTTP requests with a JSON payload, which includes the message text and some options. [Message Attachments](/docs/attachments/) can also be used in Incoming Webhooks to display richly-formatted messages that stand out from regular chat messages.

Set up an [incoming webhook integration](https://my.slack.com/services/new/incoming-webhook/) in your Slack team to try it out.

###Sending Messages

You have two options for sending data to an Incoming Webhook URL:

* Send a JSON string as the `payload` parameter in a POST request
* Send a JSON string as the body of a POST request

For a simple message, your JSON payload must contain a `text` property. This is the text that will be posted to the channel.

    {
    	"text": "This is a line of text.\nAnd this is another one."
    }

This will be displayed in the channel as:

![Screenshot of a simple incoming webhook](/img/api/incoming_simple.png)

###Adding Links

To create a link in your text, enclose the URL in `<>` angle brackets. For example: `payload={"text": "<https://slack.com>"}` will post a clickable link to https://slack.com.

To display hyperlinked text instead of the actual URL, use the pipe character, as shown in this example:

    {
    	"text": "<https://alert-system.com/alerts/1234|Click here> for details!"
    }

This will be displayed in the channel as:

![Screenshot of a simple incoming webhook with a link](/img/api/incoming_link.png)


###Customized Name and Icon

You can override an incoming webhook's configured name with the `username` parameter in your JSON payload.

You can also override the bot icon either with `icon_url` or `icon_emoji"`.

	{
	    "username": "new-bot-name",

	    "icon_url": "https://slack.com/img/icons/app-57.png",
	    "icon_emoji": ":ghost:"
	}

An overridden username and icon could look like this:

![Screenshot of a simple incoming webhook with an overridden icon and name](/img/api/incoming_name_icon.png)


###Channel Override

Incoming webhooks have a default channel. You can override it with the `channel` parameter in your JSON payload.

A public channel can be specified with `"channel": "#other-channel"`, and a Direct Message with `"channel": "@username"`.

	{
	    "channel": "#other-channel",	// A public channel override
	    "channel": "@username",			// A Direct Message override
	}

###Advanced Message Formatting

You can use [Slack's standard message markup](/docs/formatting) to add simple formatting to your messages. You can also use [message attachments](/docs/attachments) to display richly-formatted message blocks.

![Screenshot of a simple incoming webhook with an attachment](/img/api/attachment_fields.png)

###Putting it all together

Here is a sample [curl](http://curl.haxx.se/) command for posting to a channel:

    curl -X POST --data-urlencode 'payload={"text": "This is posted to <#general> and comes from *monkey-bot*.", "channel": "#general", "username": "monkey-bot", "icon_emoji": ":monkey_face:"}' https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX

This will be displayed in the #general channel as:

![Screenshot of a simple incoming webhook with an icon and links](/img/api/incoming_example.png)
