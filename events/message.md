# message event type

A `message` is delivered from several sources:

 * They are sent via the [Real Time Messaging API](/rtm) when a message is
   sent to a channel to which you subscribe. This message should immediately
   be displayed in the client.
 * They are returned via calls to [channels.history](/methods/channels.history),
   [im.history](/methods/im.history) or
   [groups.history](/methods/groups.history)
 * They are returned as `latest` property on [channel](/types/channel),
   [group](/types/group) and [im](/types/im) objects.

A simple message is self explanatory:

	{
		"type": "message",
		"channel": "C2147483705",
		"user": "U2147483697",
		"text": "Hello world",
		"ts": "1355517523.000005"
	}

The `channel` property is the ID of the channel, private group or DM channel
this message is posted in. The `user` property is the ID of the user speaking,
the `text` property is the text spoken, and `ts` is the unique (per-channel)
timestamp.

Messages can also include an `attachments` property, containing a list of
[attachment objects](/docs/attachments).

If the message has been edited after posting it will include an `edited`
property, including the user ID of the editor, and the timestamp the edit
happened. The original text of the message is not available. For example:

	{
		"type": "message",
		"channel": "C2147483705",
		"user": "U2147483697",
		"text": "Hello, world!",
		"ts": "1355517523.000005"
		"edited": {
			"user": "U2147483697",
			"ts": "1355517536.000001"
		}
	}


## Message subtypes

Unlike other event types, `message` events can have a subtype. For
example, this is a channel join message:

	{
		type: "message"
		subtype: "channel_join"
		text: "<@U023BECGF|bobby> has joined the channel"
		ts: "1403051575.000407"
		user: "U023BECGF"
	}

They are structured in this way so that clients can either support them fully
by having distinct behavior for each different subtype, or can fallback to a
simple mode by just displaying the text of the message.

The full list of message subtypes is:

{MESSAGE_SUBTYPES}

## Hidden subtypes

Some subtypes have a special hidden property. These indicate messages that
are part of the history of a channel but should not be displayed to users.
Examples include records of message edits or deletes:

	{
		"type": "message",
		"subtype": "message_deleted",
		"hidden": true,
		"channel": "C024BE91L",
		"ts": "1358878755.000001"
		"deleted_ts": "1358878749.000002",
		"event_ts": "1358878755.000002",
	}

Hidden messages are only sent over the Real Time Messaging API. They will not
appear as the `latest` property on [channel](/types/channel),
[group](/types/group) or [im](/types/im) objects. They will also not be
returned in calls to [channels.history](/methods/channels.history),
[im.history](/methods/im.history) or [groups.history](/methods/groups.history).
