# Channel Objects

A channel object contains information about a team channel.

	{
		"id": "C024BE91L",
		"name": "fun",
		"is_channel": "true",
		"created": 1360782804,
		"creator": "U024BE7LH",
		"is_archived": false,
		"is_general": false,

		"members": [
			"U024BE7LH",
			…
		],

		"topic": {
			"value": "Fun times",
			"creator": "U024BE7LV",
			"last_set": 1369677212
		},
		"purpose": {
			"value": "This channel is for fun",
			"creator": "U024BE7LH",
			"last_set": 1360782804
		}

		"is_member": true,

		"last_read": "1401383885.000061",
		"latest": { … }
		"unread_count": 0,
	}

The `name` parameter indicates the name of the channel, without a leading hash
sign.

`creator` is the user ID of the member that created this channel. `created` is
a unix timestamp.

`is_archived` will be true if the channel is archived.

`is_general` will be true if this channel is the "general" channel that
includes all regular team members. In most teams this is called `#general` but
some teams have renamed it.

`members` is a list of user ids for all users in this channel. This
includes any disabled accounts that were in this channel when they were
disabled.

`topic` and `purpose` provide information about the channel topic and purpose.

`is_member` will be true if the calling member is part of the channel.

Some API methods (such as [channels.join](/methods/channels.join)) will
include extra state information for channels when the calling user is a
member. `last_read` is the timestamp for the last message the calling user has
read in this channel. `unread_count` is a count of messages that the calling
user has yet to read. `latest` is the latest message in the channel.
