# dnd_updated_user event

    {
        "type": "dnd_updated_user",
        "user": "U1234",
        "dnd_status": {
            "dnd_enabled": true,
            "next_dnd_start_ts": 1450387800,
            "next_dnd_end_ts": 1450423800
        }
    }

The `dnd_updated_user` event is sent to all connections for a team when a user's Do Not Disturb settings have changed.
