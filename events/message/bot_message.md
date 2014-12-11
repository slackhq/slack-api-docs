# bot_message message

	{
		"type": "message",
		"subtype": "bot_message",
		"ts": "1358877455.000010",
		"text": "Pushing is the answer",
		"bot_id": "BB12033",
		"username": "github",
		"icons": {}
	}

A bot_message is sent when a message is sent to a channel by an integration
"bot". It is like a normal user message, except it has no associated user.

The `bot_id` tells you which bot sent this message, the username and icon to
use can be looked up using this. Some bot_messages also include `username`
and/or `icons` properties. If present these override the default username or
icon for this bot.
