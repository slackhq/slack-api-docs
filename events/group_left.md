# group_left event type

	{
		"type": "group_left",
		"channel": {
			…
		}
	}

The `group_left` event is sent to all connections for a user when that user
leaves a private group. Clients should respond to this message by closing the
group - this means that when a group is left from client A, it will
automatically be closed in client B.

In addition to this message, all existing members of the group will receive a
[`group_leave` message event](/events/message/group_leave).
