
Adjusts the snooze duration for a user's Do Not Disturb settings. If a snooze session is not already active for the user, invoking this method will begin one for the specified duration.

## Arguments

{ARGS}

## Response

    {
        "ok": true,
        "snooze_enabled": true,
        "snooze_endtime": 1450373897,
        "snooze_remaining": 60,
    }

The `snooze_remaining` field is expressed in seconds. If your request presents a `num_minutes` value of `1`, the response's `snooze_remaining` will be `60`.

## Errors

{ERRORS}

## Warnings

{WARNINGS}
