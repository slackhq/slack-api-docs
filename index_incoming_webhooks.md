##Send data into Slack in real-time.

Incoming Webhooks are a simple way to post messages from external sources into Slack. They make use of normal HTTP requests with a [JSON](https://en.wikipedia.org/wiki/JSON) payload that includes the message text and some options. [Message Attachments](/docs/attachments/) can also be used in Incoming Webhooks to display richly-formatted messages that stand out from regular chat messages.

Start by setting up an [incoming webhook integration](https://my.slack.com/services/new/incoming-webhook/) in your Slack team to try these features out:

1. [Sending messages](#sending_messages)
2. [Adding links](#adding_links)
3. [Customizations for custom integrations](#customizations_for_custom_integrations)
4. [Make it fancy with advanced formatting](#advanced_message_formatting)
5. [Putting it all together](#putting_it_all_together)
6. [Distributing as a Slack app](#share_your_incoming_webhook_as_a_slack_app)

Use [**curl**](http://curl.haxx.se/), a simple, ubiquitous tool for sending HTTP requests on the command line, for the *curl examples* that follow.

###Sending messages

Let's learn how to send this in-channel message as an incoming webhook:

![Screenshot of a simple incoming webhook](/img/api/incoming_simple.png)

It's a simple, multi-line message without special formatting:

    This is a line of text.
    And this is another one.

The first step is to prepare this message as a key/value pair in JSON. For a simple message, your JSON payload only needs to define a `text` property, containing the text that will be posted to the channel.

In JSON, our message is defined as:

    {
        "text": "This is a line of text.\nAnd this is another one."
    }

Please note that we indicated the line break as the control character `\n`. We also added additional whitespace for readability, which we could have more tidily presented to you as:

    {"text":"This is a line of text.\nAnd this is another one."}

Once you've put together the JSON for your message, you can choose to send it to your Incoming Webhook URL one of two ways:

#### Send it directly in JSON

The preferred way to send Slack your JSON body is by sending a HTTP POST to your webhook URL, containing a request body with an explicit `Content-type` HTTP header set to `application/json`. This tells Slack how to interpret the data you're sending us.

    POST https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
    Content-type: application/json
    {
        "text": "This is a line of text.\nAnd this is another one."
    }

By declaring the content type, no further encoding of the POST body is needed &mdash; just provide valid JSON in UTF-8.

<div class="example rounded no_padding">
<h5>curl example <i class="ts_icon ts_icon_code"></i></h5>
<pre class="small code_wrap top_margin">curl -X POST -H 'Content-type: application/json' --data '{"text":"This is a line of text.\nAnd this is another one."}' https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX</pre>
</div>

#### Send a JSON string within a parameter of a standard POST request

If you want to stick with the more traditional `Content-type` of `application/x-www-form-urlencoded`, you can sneakily send URL-escaped JSON within the `payload` parameter instead.

Send the `payload` parameter as part of your POST body and explicitly state the `Content-type`. Payloads should not be included as query parameters on the webhook URL.

The trickiest part of this approach is that you must properly [URL encode](https://tools.ietf.org/html/rfc3986) your `payload`. Your elegant JSON message becomes seeming nonsense, filled with percent-encoded characters.

    POST https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
    Content-type: application/x-www-form-urlencoded
    payload=%7B%22text%22%3A%22This%20is%20a%20line%20of%20text.%5CnAnd%20this%20is%20another%20one.%22%7D

Many HTTP clients provide convenient functions for URL encoding and setting the `Content-type`.

<div class="example rounded no_padding">
<h5>javascript example <i class="ts_icon ts_icon_code"></i></h5>
<pre class="small code_wrap top_margin">var webhook_url = 'https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX';
var request = new XMLHttpRequest(); 
// important: replace #myChannel with the name of your channel. Keep the # sign
var json = 'payload={"channel": "#myChannel", "username": "myBot", "text": "This is a line of text.\nAnd this is another one."}'; 
request.open('POST', webhook_url, false); 
request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
request.send(json);
</pre>
</div>

<div class="example">
<h5>curl example <i class="ts_icon ts_icon_code"></i></h5>
<pre class="small code_wrap top_margin">curl -X POST --data-urlencode 'payload={"text":"This is a line of text.\nAnd this is another one."}' https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX</pre>
</div>

Using the `--data-urlencode` curl parameter automatically URL encodes the provided string.

---

###Adding links

To create a link in your text, enclose the URL in `<>` angle brackets. For example: `payload={"text": "<https://slack.com>"}` will post a clickable link to https://slack.com.

To display hyperlinked text instead of the actual URL, use the pipe character, as shown in this example:

    {
        "text": "<https://alert-system.com/alerts/1234|Click here> for details!"
    }

This will be displayed in the channel as:

![Screenshot of a simple incoming webhook with a link](/img/api/incoming_link.png)

### Customizations for custom integrations

Though it is best to use a single incoming webhook for a specific purpose, in some cases you may want to override the default channel and authoring identity of an incoming webhook.

<p class="alert alert_info"><i class="ts_icon ts_icon_info_circle"></i> You <strong>cannot override</strong> the default username, icon, or channel for incoming webhooks attached to <a href="/slack-apps">Slack apps</a>. Instead, these values will stubbornly inherit from the associated Slack app configuration.</p>

####Customizing your username and icon

Incoming webhooks originate from a default identity you configured when originally creating your webhook. You can override a custom integration's configured name with the `username` field in your JSON payload.

You can also override the bot icon either with `icon_url` or `icon_emoji`.

    {
        "username": "ghost-bot",
        "icon_emoji": ":ghost:",
        "text": "BOO!"
    }

An overridden username and icon could look like this:

![Screenshot of a simple incoming webhook with an overridden icon and name](/img/api/incoming_name_icon.png)

####Channel override

Incoming webhooks output to a default channel and can only send messages to a single channel at a time. You can override a custom integration's configured channel by specifying the `channel` field in your JSON payload.

Specify a Slack channel by name with `"channel": "#other-channel"`, or send a Slackbot message to a specific user with `"channel": "@username"`.

    {
        "channel": "#other-channel",
        "text": "This message will appear in #other-channel"
    }

If you prefer, you can also specify a channel ID or user ID like so: `"channel": "U024BE7LH"`.

---

###Advanced message formatting

You can use [Slack's standard message markup](/docs/formatting) to add simple formatting to your messages. You can also use [message attachments](/docs/attachments) to display richly-formatted message blocks.

![Screenshot of a simple incoming webhook with an attachment](/img/api/attachment_fields.png)

###Putting it all together

Here is a sample [curl](http://curl.haxx.se/) command for posting to a channel using the payload parameter:

<div class="example">
<h5>curl example <i class="ts_icon ts_icon_code"></i></h5>
<pre class="small code_wrap top_margin">curl -X POST --data-urlencode 'payload={"text": "This is posted to <#general> and comes from *monkey-bot*.", "channel": "#general", "username": "monkey-bot", "icon_emoji": ":monkey_face:"}' https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX</pre>
</div>

And here is a version using a `Content-type` of `application/json`:

<div class="example">
<h5>curl example <i class="ts_icon ts_icon_code"></i></h5>
<pre class="small code_wrap top_margin">curl -X POST -H 'Content-type: application/json' --data '{"text": "This is posted to <#general> and comes from *monkey-bot*.", "channel": "#general", "username": "monkey-bot", "icon_emoji": ":monkey_face:"}' https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX</pre>
</div>

With either approach, this will be displayed in the #general channel as:

![Screenshot of a simple incoming webhook with an icon and links](/img/api/incoming_example.png)

###Share your incoming webhook as a Slack app
You will be able to set up an incoming webhook when you create a [Slack app](/slack-apps) and configure a [Slack button](/docs/slack-button).

Once a user installs your app, you will exchange the `code` for an access token using [the `oauth.access` method](https://api.slack.com/methods/oauth.access). The JSON response from this API call will contain the access token and incoming webhook URL:


    {
        "access_token": "xoxp-XXXXXXXX-XXXXXXXX-XXXXX",
        "scope": "incoming-webhook",
        "team_name": "Team Installing Your Hook",
        "incoming_webhook": {
            "url": "https://hooks.slack.com/TXXXXX/BXXXXX/XXXXXXXXXX",
            "channel": "#channel-it-will-post-to",
            "channel_id": "C05002EAE",
            "configuration_url": "https://teamname.slack.com/services/BXXXXX"
        }
    }

Keep in mind that incoming webhooks packaged as Slack apps cannot override the default channel, username, or icon associated with the webhook.

**[Create a Slack app](/slack-apps)** to package and distribute your incoming webhook and share it in our [application directory](https://slack.com/apps).
