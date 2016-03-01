# User Group Objects

A user group object contains information about a group of users.

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
        "users": [
            "U060RNRCZ",
            "U060ULRC0",
            "U06129G2V",
            "U061309JM"
        ],
        "user_count": "4"
    }

The `name` parameter indicates the friendly name of the group.

For disabled groups, `date_deleted` will be non-zero.

The `description` parameter explains the purpose of the group (optional).

The `handle` parameter indicates the value used to notify group members via a mention without a leading @ sign.

The `auto_type` parameter can be `admins` for a Team Admins group, `owners` for a Team Owners group or `null` for a custom group.

The `prefs` parameter contains default `channels` and `groups` (private channels) that members of this group will be invited to upon joining.

The `users` parameter contains a list of [user object](/types/user) `id` values which belong to the user group. This parameter is included if the `include_users` option is enabled on some API endpoints.

The `user_count` parameter indicates the total number of users in a group.
