This method takes an existing private group and performs the following steps:

 * Renames the existing group (from "example" to "example-archived").
 * Archives the existing group.
 * Creates a new group with the name of the existing group.
 * Adds all members of the existing group to the new group.

This is useful when inviting a new member to an existing group while hiding
all previous chat history from them. In this scenario you can call
`groups.createChild` followed by `groups.invite`.

The new group will have a special `parent_group` property pointing to the
original archived group. This will only be returned for members of both
groups, so will not be visible to any newly invited members.


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
