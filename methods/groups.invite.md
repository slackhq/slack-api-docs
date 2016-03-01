This method is used to invite a user to a private channel. The calling user must be a member of the private channel.

To invite a new member to a private channel without giving them access to the archives
of the private channel, call the [`groups.createChild` method](/methods/groups.createChild)
before inviting.

## Arguments

{ARGS}


## Response

If successful, the API response includes a [group object](/types/group):

    {
        "ok": true,
        "group": {
            …
        },
    }

If the invited user is already in the private channel, the response will include an
`already_in_group` property:

    {
        "ok": true,
        "already_in_group": true,
        "group": {
            …
        },
    }


## Errors

{ERRORS}

## Warnings

{WARNINGS}
