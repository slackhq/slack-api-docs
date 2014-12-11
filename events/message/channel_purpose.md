# channel_purpose message

	{
		"type": "message",
		"subtype": "channel_purpose",
		"ts": "1358877455.000010",
		"user": "U2147483828",
		"purpose": "whatever",
		"text": "<@U2147483828|cal> set the channel purpose: whatever"
	}

A `channel_purpose` message is sent when the purpose for a channel is changed
using the [`channel.setPurpose` method](/methods/channel.setPurpose).
