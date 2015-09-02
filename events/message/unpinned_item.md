# unpinned_item message

	{
		"type": "message",
		"subtype": "unpinned_item",
		"user": "USLACKBOT",
		"item_type": "G",
		"text": "<@U024BE7LH|cal> unpinned the message you pinned to the secretplans group.",
		"item": {
			…
		},
		"channel": "G024BE91L",
		"ts": "1360782804.083113"
	}

When an item is un-pinned from a channel, an `unpinned_item` message is sent via slackbot to the user that initially pinned the item. The message will only be sent if the item was un-pinned by a different user.

Valid `item_type` values include:

 * `C`: channel message
 * `G`: private group message
 * `F`: file
 * `Fc`: file comments
