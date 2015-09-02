
This method returns a list of all reactions for a single item (file, file comment, channel message, group message, or direct message).

## Arguments

{ARGS}


## Response

The response contains the item with reactions.

	{
		"type": "message",
		"channel": "C2147483705",
		"message": {
			...
			"reactions": [
				{
					"name": "astonished",
					"count": 3,
					"users": [ "U1", "U2", "U3" ]
				},
				{
					"name": "clock1"
					"count": 2,
					"users": [ "U1", "U2", "U3" ]
				}
			]
		},
	},

Different item types can be reacted to. The item returned has a `type` property, the
other properties depend on the type of item. The possible types are:

 * **`message`**: the item will have a `message` property containing a [message object](/docs/messages) and a `channel` property containing the channel ID for the message.
 * **`file`**: this item will have a `file` property containing a [file object](/types/file).
 * **`file_comment`**: the item will have a `file` property containing the [file object](/types/file) and a `comment` property containing the file comment.

The users array in the `reactions` property might not always contain all users that have reacted (we limit it to X users, and X might change), however `count` will always represent the count of all
users who made that reaction (i.e. it may be greater than `users.length`). If the authenticated user has a given reaction then they are guaranteed to appear in the `users` array, regardless of
whether `count` is greater than `users.length` or not. If the complete list of users is required they can still be obtained by specifying the `full` argument.

## Errors

{ERRORS}