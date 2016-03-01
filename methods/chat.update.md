This method updates a message in a channel. Though related to [`chat.postMessage`](/methods/chat.postMessage), some parameters of `chat.update` are handled differently.


## Arguments

{ARGS}

## Formatting

The default value for parse will attempt to discover links in text but does not support URL markup. To update messages with URL markup, you must specify `parse=none`. For more information, refer to the [formatting spec](/docs/formatting).

To use `link_names`, you'll need to explicitly set the `parse` parameter to `full`.

The optional `attachments` argument should contain a JSON-encoded array of attachments. If you do not include an attachments property,
a message's previous attachments will remain visible. To remove a previous attachment, include an empty `attachments` array with your request. For more information, see the [attachments spec](/docs/attachments).

## Valid message types

Only messages posted by the authenticated user are able to be updated using this method. This includes regular chat messages, as well as messages containing the `me_message` subtype.

Attempting to update other message types will return a `cant_update_message` error.

## Response

    {
        "ok": true,
        "channel": "C024BE91L",
        "ts": "1401383885.000061",
        "text": "Updated Text"
    }

The response includes the `text`, `channel` and `timestamp` properties of the
updated message so clients can keep their local copies of the message in sync.

## Bot users

To use `chat.update` with a [bot user](/bot-users) token, you'll need to _think of your bot user as a user_, and pass `as_user` set to `true` while editing a message created by that same bot user.

## Errors

{ERRORS}

## Warnings

{WARNINGS}
