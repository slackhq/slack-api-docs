## Customized commands for your team

Slash commands listen for custom triggers in chat messages across all Slack channels. When a slash command is triggered, a payload will be sent to an external URL.

For example, typing **/weather 94070** could send a message to an external URL that would look up the current weather forecast for San Francisco and post it back to the user in Slack.

Set up a [slash command](https://my.slack.com/services/new/slash-commands/) in your Slack team to try it out.

###Outgoing Data

When a matching chat message is received, a POST will be sent to the specified URL.

The POST data sent along is defined as follows:

	token=gIkuvaNzQIHg97ATvDxqgjtO
	team_id=T0001
	team_domain=example
	channel_id=C2147483705
	channel_name=test
	user_id=U2147483697
	user_name=Steve
	command=/weather
	text=94070

###Responding

The URL _should_ respond with the text to reply to the user unless no response is necessary. Any non-200 response will result in an error to the user.

The response from a slash command will only be visible to the user that issued the command.  If the command needs to post to a channel so that all members can see it, the handler should do that outside of the response — perhaps by using [Incoming Webhooks](/incoming-webhooks).

###GET Requests

If you prefer, the request can be sent as a GET by choosing that option in the integration's settings. In that case, the payload would be sent like so:

    https://your-url.com/path/to/handler?token=gIkuvaNzQIHg97ATvDxqgjtO&team_id=T0001&…
