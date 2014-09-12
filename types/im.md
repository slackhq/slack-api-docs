# IM Objects

An IM object contains information about a direct message channel.

    {
        "id": "D024BFF1M",
        "is_im": true,
        "user": "U024BE7LH",
        "created": "1360782804",
        "is_user_deleted": false
    },

Each direct message channel is between two users. One of these users is always
the calling user, the other is indicated by the `user` property.
`is_user_deleted` will be true if the other user's account has been disabled.

`created` is a unix timestamp.

Some API methods will include extra state information for the channel.
`is_open` shows if the DM channel is open. `last_read` is the timestamp for the
last message the calling user has read in this channel. `unread_count` is a
count of messages that the calling user has yet to read. `latest` is the
latest message in the channel.
