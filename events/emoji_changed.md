# emoji_changed event type

	{
		"type": "emoji_changed",
		"event_ts" : "1361482916.000004"
	}

The `emoji_changed` event is sent to all connections for a team when that
team's custom emoji is updated. When they receive this event, clients should
update their local cache of emoji by calling
[the emoji.list method](/methods/emoji.list) again.
