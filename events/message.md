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
		"ts": "1355517523.000005",
		"edited": {
			"user": "U2147483697",
			"ts": "1355517536.000001"
		}
	}


## Message subtypes

Unlike other event types, `message` events can have a subtype. For
example, this is a channel join message:

	{
		type: "message",
		subtype: "channel_join",
		text: "<@U023BECGF|bobby> has joined the channel",
		ts: "1403051575.000407",
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
		"ts": "1358878755.000001",
		"deleted_ts": "1358878749.000002",
		"event_ts": "1358878755.000002"
	}

Hidden messages are only sent over the Real Time Messaging API. They will not
appear as the `latest` property on [channel](/types/channel),
[group](/types/group) or [im](/types/im) objects. They will also not be
returned in calls to [channels.history](/methods/channels.history),
[im.history](/methods/im.history) or [groups.history](/methods/groups.history).

## Stars, pins, and reactions

Messages can have several extra properties depending on whether or not they have
been starred, pinned, or reacted to:

	{
		"type": "message",
		"channel": "C2147483705",
		"user": "U2147483697",
		"text": "Hello world",
		"ts": "1355517523.000005",
		"is_starred": true,
		"pinned_to": ["C024BE7LT", ...],
		"reactions": [
			{
				"name": "astonished",
				"count": 3,
				"users": [ "U1", "U2", "U3" ]
			},
			{
				"name": "facepalm",
				"count": 1034,
				"users": [ "U1", "U2", "U3", "U4", "U5" ]
			}
		]
	}

The `is_starred` property is present and true if the calling user has starred the message, else
it is omitted.

The `pinned_to` array, if present, contains the IDs of any channels to which the message is currently pinned.

The `reactions` property, if present, contains any reactions that have been added to the message and gives information about the
type of reaction, the total number of users who added that reaction and a (possibly incomplete) list of users who have
added that reaction to the message. The users array in the `reactions` property might not always contain all users
that have reacted (we limit it to X users, and X might change), however `count` will always represent the count of all
users who made that reaction (i.e. it may be greater than `users.length`). If the authenticated user has a given reaction
then they are guaranteed to appear in the `users` array, regardless of whether `count` is greater than `users.length` or not.
