This method returns a list of all user groups in the team. This can optionally include disabled user groups.

## Arguments

{ARGS}

## Response

Returns a list of [usergroup objects](/types/usergroup), in no particular order:

    {
        "ok": true,
        "usergroups": [
            {
                "id": "S0614TZR7",
                "team_id": "T060RNRCH",
                "is_usergroup": true,
                "name": "Team Admins",
                "description": "A group of all Administrators on your team.",
                "handle": "admins",
                "is_external": false,
                "date_create": 1446598059,
                "date_update": 1446670362,
                "date_delete": 0,
                "auto_type": "admin",
                "created_by": "USLACKBOT",
                "updated_by": "U060RNRCZ",
                "deleted_by": null,
                "prefs": {
                    "channels": [

                    ],
                    "groups": [

                    ]
                },
                "user_count": "2"
            },
            {
                "id": "S06158AV7",
                "team_id": "T060RNRCH",
                "is_usergroup": true,
                "name": "Team Owners",
                "description": "A group of all Owners on your team.",
                "handle": "owners",
                "is_external": false,
                "date_create": 1446678371,
                "date_update": 1446678371,
                "date_delete": 0,
                "auto_type": "owner",
                "created_by": "USLACKBOT",
                "updated_by": "USLACKBOT",
                "deleted_by": null,
                "prefs": {
                    "channels": [

                    ],
                    "groups": [

                    ]
                },
                "user_count": "1"
            },
            {
                "id": "S0615G0KT",
                "team_id": "T060RNRCH",
                "is_usergroup": true,
                "name": "Marketing Team",
                "description": "Marketing gurus, PR experts and product advocates.",
                "handle": "marketing-team",
                "is_external": false,
                "date_create": 1446746793,
                "date_update": 1446747767,
                "date_delete": 1446748865,
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
        ]
    }

## Errors

{ERRORS}

## Warnings

{WARNINGS}
