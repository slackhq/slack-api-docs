This method creates a private group.


## Arguments

{ARGS}


## Response

If successful, the command returns a [group object](/types/group), including state information:

    {
        "ok": true,
        "group": {
            "id": "G024BE91L",
            "name": "secretplans",
            "is_group": "true",
            "created": "1360782804",
            "creator": "U024BE7LH",
            "is_archived": false,
            "is_open": true,
            "last_read": "0000000000.000000",
            "latest": null,
            "unread_count": 0,
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
        }
    }


## Errors

{ERRORS}


