This method enables a user group which was previously disabled.

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
            "date_update": 1446747767,
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

When a user group is enabled, it's `date_delete` parameter will be `0` (zero).

## Errors

{ERRORS}

## Warnings

{WARNINGS}
