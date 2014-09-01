# Channel messages

Channel messages are sent to a channel, IM or Group, delivered from several sources:

* Sent by the message server, over the websocket.
* Returned via calls to `channel.history`, `im.history` or `group.history`.
* Returned as the `latest` message for channels/ims/groups, during login or joining.


## Messages

The most simple message is regular text from a user:

	{
		"type": "message",
		"ts": "1358878749.000002",
		"user": "U2147483828",
		"text": "hi"
	}

Other messages that need to be displayed in some way will have the following structure:

	{
		"type": "message",
		"ts": "1358878749.000002",
		"subtype": "something",
		"text": "hi",
		...more...
	}

They are structured in this way so that clients can either support them fully (by having distinct 
behavior for each different `subtype`) or can fallback to a simple mode by just showing the `text` of 
the message. Note that these messages do not come from a user. Message text is typically automatically 
generated to explain the event, but a full client will format this information specially. The message
text supports the usual [user, channel and URL escaping](/docs/formatting).

Messages may optionally include [attachments](/docs/attachments) for display of structured data.

Messages that are part of a channel's history, but should not be displayed to the user, have a special
`hidden` flag. These messages include records of edits and deletes and other 'invisible' metadata.

	{
		"type": "message",
		"ts": "1358878749.000002",
		"subtype": "message_changed",
		"hidden": true,
		...more...
	}


## Invisible message subtypes

The contents of a message changed

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

A message was removed

	{
		"type": "message",
		"subtype": "message_deleted",
		"hidden": true,
		"channel": "C2147483705",
		"ts": "1358878755.000001"
		"deleted_ts": "1358878749.000002",
	}


## Visible message subtypes

New member has been joined to a channel

	{
		"type": "message",
		"subtype": "channel_join",
		"ts": "1358877458.000011",
		"user": "U2147483828",
		"text": "<@U2147483828|cal> has joined the channel"
	}

Existing member has left a channel

	{
		"type": "message",
		"subtype": "channel_leave",
		"ts": "1358877455.000010",
		"user": "U2147483828",
		"text": "<@U2147483828|cal> has left the channel"
	}

Channel topic change

	{
		"type": "message",
		"subtype": "channel_topic",
		"ts": "1358877455.000010",
		"user": "U2147483828",
		"topic": "hello world",
		"text": "<@U2147483828|cal> set the channel topic: hello world"
	}

Channel purpose change

	{
		"type": "message",
		"subtype": "channel_purpose",
		"ts": "1358877455.000010",
		"user": "U2147483828",
		"purpose": "whatever",
		"text": "<@U2147483828|cal> set the channel purpose: whatever"
	}

"Bot" messages

	{
		"type": "message",
		"subtype": "bot_message",
		"ts": "1358877455.000010",
		"text": "[SlackClientSpec/master] added presence to users for login message - Cal Henderson 
			(https://github.com/tinyspeck/SlackClientSpec/commit/82276fd02393e0571c38289ab887ed84f92a9519)",
		"bot_id": "BB12033", // optional bot id that defines the name and icons to use for this message
		"username": "github", // optional name for the bot to "speak" as, should only be used if `bot_id` is not present
		"icons": {} // optional hash of icons to use for displaying the bot (overrides what is set in `bot_id`)
	}

File shared with channel

	{
		"type": "message",
		"subtype": "file_share",
		"ts": "1358877455.000010",
		"text": "<@cal> uploaded a file: <https:...7.png|7.png>",
		"file": {...},
		"user": "U2147483697",
		"upload": true
	}

Comment on a file

	{
		"type": "message",
		"subtype": "file_comment",
		"ts": "1361482916.000003",
		"text": "<@cal> commented on a file: ...",
		"file": {},
		"comment": {}
	}

Channel archived

	{
		"type": "message",
		"subtype": "channel_archive",
		"ts": "1361482916.000003",
		"text": "<U1234|@cal> archived the channel",
		"user": "U1234",
		"members": ["U1234", "U5678", ...]
	}

Channel un-archived

	{
		"type": "message",
		"subtype": "channel_unarchive",
		"ts": "1361482916.000003",
		"text": "<U1234|@cal> un-archived the channel",
		"user": "U1234"
	}

The following subtypes for groups take exactly the same format as their `channel_*` equivalents:

* `group_join`
* `group_leave`
* `group_topic`
* `group_purpose`
* `group_archive` (does not contain a `members` array)
* `group_unarchive`
