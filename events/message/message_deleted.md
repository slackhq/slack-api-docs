# message_deleted message

	{
		"type": "message",
		"subtype": "message_deleted",
		"hidden": true,
		"channel": "C2147483705",
		"ts": "1358878755.000001",
		"deleted_ts": "1358878749.000002"
	}

A `message_deleted` message is sent when a message in a channel is deleted,
usually via the [`chat.delete` method](/methods/chat.delete).

The `deleted_ts` property gives the timestamp of the message that was deleted.

If clients find an existing message with the same `deleted_ts` and `channel`,
the existing message should be removed from the local model and UI. The
original message will no longer return in history calls.

All types of messages are eligible for deletion, not just user-sent messages.
