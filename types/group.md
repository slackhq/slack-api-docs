# Group Objects

A group object contains information about a private group.

    {
        "id": "G024BE91L",
        "name": "secretplans",
        "is_group": "true",
        "created": "1360782804",
        "creator": "U024BE7LH",
        "is_archived": false,
        "members": [
            "U024BE7LH"
        ],
        "topic": {
            "value": "Secret plans on hold",
            "creator": "U024BE7LV",
            "last_set": "1369677212"
        },
        "purpose": {
            "value": "Discuss secret plans that no-one else should know",
            "creator": "U024BE7LH",
            "last_set": "1360782804"
        }

    },

The `name` parameter indicates the name of the group.

`creator` is the user ID of the member that created this group. `created` is
a unix timestamp.

`is_archived` will be true if the group is archived.

`members` is a list of user ids for all users in this group. This
includes any disabled accounts that were in this group when they were
disabled.

`topic` and `purpose` provide information about the group topic and purpose.

Some API methods will include extra state information for the group.
`is_open` shows if the group is open. `last_read` is the timestamp for the
last message the calling user has read in this group. `unread_count` is a
count of messages that the calling user has yet to read. `latest` is the
latest message in the group.
