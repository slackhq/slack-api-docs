This method starts a Real Time Messaging API session. Refer to the
[RTM API documentation](/rtm) for full details on how to use the RTM API.

## Arguments

{ARGS}


## Response

This method returns lots of data about the current state of a team, along
with a WebSocket Message Server URL:

    {
        "ok": true,
        "url": "wss:\/\/ms9.slack-msgs.com\/websocket\/7I5yBpcvk",

        "self": {
            "id": "U023BECGF",
            "name": "bobby",
            "prefs": {
                …
            },
            "created": 1402463766,
            "manual_presence": "active"
        },
        "team": {
            "id": "T024BE7LD",
            "name": "Example Team",
            "email_domain": "",
            "domain": "example",
            "icon": {
                …
            },
            "msg_edit_window_mins": -1,
            "over_storage_limit": false
            "prefs": {
                …
            },
            "plan": "std"
        },
        "users": [ … ],

        "channels": [ … ],
        "groups": [ … ],
        "mpims": [ … ],
        "ims": [ … ],

        "bots": [ … ],
    }

The `url` property contains a WebSocket Message Server URL. Connecting to this
URL will initiate a Real Time Messaging session. These URLs are only valid for
30 seconds, so connect quickly!

The `self` property contains details on the authenticated user.

The `team` property contains details on the authenticated user's team. If a team has
not yet set a custom icon, the value of `team.icon.image_default` will be `true`.

The `users` property contains a list of [user objects](/types/user), one for every
member of the team.

The `channels` property is a list of [channel objects](/types/channel), one
for every channel visible to the authenticated user. For regular or
administrator accounts this list will include every team channel. The
`is_member` property indicates if the user is a member of this channel. If
true then the channel object will also include the topic, purpose, member
list and read-state related information.

The `groups` property is a list of [group objects](/types/group), one for
every group the authenticated user is in.

The `mpims` property is a list of [mpims objects](/types/mpim), one for
every group the authenticated user is in.  MPIMs are only returned to the client
if `mpim_aware` is set when calling `rtm.start`.  Otherwise, `mpims` are emulated
using the groups API.

The `ims` property is a list of
[IM objects](/types/im), one for every direct message channel visible to the
authenticated user.

The `bots` property gives details of the integrations set up on this team.


## Errors

{ERRORS}

## Warnings

{WARNINGS}
