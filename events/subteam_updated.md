# subteam_updated event

    {
        "type": "subteam_updated",
        "subteam": {
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
    }

The `subteam_updated` event is sent to all connections for a team when
an existing user group is updated. This event is triggered for changes
to the user group information (name, description, or handle) as well as
the members of the group. Clients can use this to update their local
list of groups and group members.
