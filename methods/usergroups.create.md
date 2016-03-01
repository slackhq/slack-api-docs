This method is used to create a user group.

## Arguments

{ARGS}

## Response

If successful, the command returns a [usergroup object](/types/usergroup), including preferences:

    {
        "ok": true,
        "usergroup": {
            "id": "S0615G0KT",
            "team_id": "T060RNRCH",
            "is_usergroup": true,
            "name": "Marketing Team",
            "description": "Marketing gurus, PR experts and product advocates.",
            "handle": "marketing-team",
            "is_external": false,
            "date_create": 1446746793,
            "date_update": 1446746793,
            "date_delete": 0,
            "auto_type": null,
            "created_by": "U060RNRCZ",
            "updated_by": "U060RNRCZ",
            "deleted_by": null,
            "prefs": {
                "channels": [

                ],
                "groups": [

                ]
            },
            "user_count": "0"
        }
    }

## Errors

{ERRORS}

## Warnings

{WARNINGS}
