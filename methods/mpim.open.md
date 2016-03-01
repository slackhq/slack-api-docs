This method opens a multiparty direct message.

Opening a multiparty direct message takes a list of up-to 8 encoded user ids.  If there is no MPIM already created that
includes that exact set of members, a new MPIM will be created.  Subsequent calls to `mpim.open` with the same set of
users will return the already existing MPIM conversation.


## Arguments

{ARGS}


## Response

If successful, the command returns a [mpim object](/types/mpim), including state information:

    {
        "ok": true,
        "group": {
            "id": "G024BE91L",
            "name": "mpdm-user--user_a--user_b--user_c-1",
            "is_group": "true",
            "created": 1360782804,
            "creator": "U024BE7LH",
            "is_archived": false,
            "is_open": false,
            "is_mpim": true,
            "last_read": "0000000000.000000",
            "latest": null,
            "unread_count": 0,
            "unread_count_display": 0,
            "members": [
                "U024BE7LH",
                "U1234567890",
                "U2345678901",
                "U3456789012"
            ],
            "topic": {
                "value": "Group messaging.",
                "creator": "U024BE7LH",
                "last_set": 1360782804
            },
            "purpose": {
                "value": "Group messaging with: @user @user_a @user_b @user_c",
                "creator": "U024BE7LH",
                "last_set": 1360782804
            }
        }
    }


## Errors

{ERRORS}



## Warnings

{WARNINGS}
