This method takes an existing private channel and performs the following steps:

 * Renames the existing private channel (from "example" to "example-archived").
 * Archives the existing private channel.
 * Creates a new private channel with the name of the existing private channel.
 * Adds all members of the existing private channel to the new private channel.

This is useful when inviting a new member to an existing private channel while hiding
all previous chat history from them. In this scenario you can call
`groups.createChild` followed by `groups.invite`.

The new private channel will have a special `parent_group` property pointing to the
original archived private channel. This will only be returned for members of both
private channels, so will not be visible to any newly invited members.


## Arguments

{ARGS}


## Response

If successful, the command returns the new [group object](/types/group):

    {
        "ok": true,
        "group": {
            "id": "G024BE91L",
            "name": "secretplans",
            "is_group": "true",
            "created": 1360782804,
            "creator": "U024BE7LH",
            "is_archived": false,
            "members": [
                "U024BE7LH"
            ],
            …
        }
    }


## Errors

{ERRORS}

## Warnings

{WARNINGS}
