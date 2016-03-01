# message_changed message

	{
		"type": "message",
		"subtype": "message_changed",
		"hidden": true,
		"channel": "C2147483705",
		"ts": "1358878755.000001",
		"message": {
			"type": "message",
			"user": "U2147483697",
			"text": "Hello, world!",
			"ts": "1355517523.000005",
			"edited": {
				"user": "U2147483697",
				"ts": "1358878755.000001"
			}
		}
    }

A `message_changed` message is sent when a message in a channel is edited
using the [`chat.update` method](/methods/chat.update). The `message` property
contains the updated message object.

When clients receive this message type, they should look for an existing
message with the same `message.ts` in that `channel`. If they find one the
existing message should be replaced with the new one.
