# MPIM Objects

A mpim object contains information about a multiparty IM.

    {
        "id": "G024BE91L",
        "name": "mpdm-user1--user2--user3-1",
		"is_mpim": true,
        "is_group": false,
        "created": 1360782804,
        "creator": "U024BE7LH",
        "members": [
            "U024BE7LH"
        ],
        "last_read": "1401383885.000061",
        "latest": { … }
        "unread_count": 0,
        "unread_count_display": 0

    },


The `name` parameter indicates the name of the mpim.

`creator` is the user ID of the member that created this mpim. `created` is
a unix timestamp.

`members` is a list of user ids for all users in this mpim. This
includes any disabled accounts that were in this mpim when they were
disabled.

`is_mpim` is a boolean that indicated if a multiparty im (`mpim`) is being
emulated as a group.  For compatibility with older clients, `mpims` can
appear as groups unless `rtm.start` is called with `mpim_aware=1`.