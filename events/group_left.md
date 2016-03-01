# group_left event type

    {
        "type": "group_left",
        "channel": "G02ELGNBH"
    }

The `group_left` event is sent to all connections for a user when that user
leaves a private channel. Clients should respond to this message by closing the
private channel - this means that when a private channel is left from client A, it will automatically be closed in client B.

The `channel` value is the string identifier for the private channel.

In addition to this message, all existing members of the group will receive a
[`group_leave` message event](/events/message/group_leave).
