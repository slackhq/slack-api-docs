# Group Objects

A group object contains information about a private channel. Private channels were once known as "private groups." Consider a group object the same thing as a private channel object.

    {
        "id": "G024BE91L",
        "name": "secretplans",
        "is_group": "true",
        "created": 1360782804,
        "creator": "U024BE7LH",
        "is_archived": false,
        "is_mpim": false,
        "members": [
            "U024BE7LH"
        ],
        "topic": {
            "value": "Secret plans on hold",
            "creator": "U024BE7LV",
            "last_set": 1369677212
        },
        "purpose": {
            "value": "Discuss secret plans that no-one else should know",
            "creator": "U024BE7LH",
            "last_set": 1360782804
        },

        "last_read": "1401383885.000061",
        "latest": { … }
        "unread_count": 0,
        "unread_count_display": 0

    },

The `name` parameter indicates the name of the private channel.

`creator` is the user ID of the member that created this private channel. `created` is
a unix timestamp.

`is_archived` will be true if the private channel is archived.

`members` is a list of user ids for all users in this private channel. This
includes any disabled accounts that were in this private channel when they were
disabled.

`mpims` is a boolean that indicated if a multiparty im (`mpim`) is being
emulated as a private channel.  For compatibility with older clients, `mpims` can
appear as private channels unless `rtm.start` is called with `mpim_aware=1`.

`topic` and `purpose` provide information about the private channel topic and purpose.

Some API methods (such as [groups.create](/methods/groups.create)) will
include extra state information for channels when the calling user is a
member. `last_read` is the timestamp for the last message the calling user has
read in this channel. `unread_count` is a full count of visible messages that the 
calling user has yet to read. `unread_count_display` is a count of messages that
the calling user has yet to read that matter to them (this means it excludes things
like join/leave messages). `latest` is the latest message in the channel.
