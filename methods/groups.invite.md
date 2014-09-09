This method is used to invite a user to a private group. The calling user must be a member of the group.

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

If the invited user is already in the group, the response will include an
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
