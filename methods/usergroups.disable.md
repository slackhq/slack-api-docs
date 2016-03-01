This method disables an existing user group.

## Arguments

{ARGS}

## Response

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
            "date_update": 1446747568,
            "date_delete": 1446747568,
            "auto_type": null,
            "created_by": "U060RNRCZ",
            "updated_by": "U060RNRCZ",
            "deleted_by": "U060RNRCZ",
            "prefs": {
                "channels": [

                ],
                "groups": [

                ]
            },
            "user_count": "0"
        }
    }

When a user group has been disabled it's `date_delete` parameter will be non-zero.

## Errors

{ERRORS}

## Warnings

{WARNINGS}
