
Edit an existing comment on a file. Only the user who created a comment may make edits. Teams may configure a limited time window during which file comment edits are allowed.


## Arguments

{ARGS}

## Response

If successful, the response will include a file comment object.

    {
        "ok": true,
        "comment": {
            "id": "Fc1234567890",
            "created": 1356032811,
            "timestamp": 1356032811,
            "user": "U1234567890",
            "comment": "Everyone should take a moment to read this file, seriously."
        }
    }

## Errors

{ERRORS}

## Warnings

{WARNINGS}
