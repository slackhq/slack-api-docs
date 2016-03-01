# group_rename event type

    {
        "type": "group_rename",
        "channel": {
            "id":"G02ELGNBH",
            "name":"new_name",
            "created":1360782804
        }
    }

When a private channel is renamed, the `group_rename` event is sent to all connections for members of a private channel. Clients can use this to update their local list of private channels.
