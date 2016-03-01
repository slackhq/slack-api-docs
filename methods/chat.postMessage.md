
This method posts a message to a public channel, private group, or IM channel.


## Arguments

{ARGS}

## Formatting

Messages are formatted as described in the [formatting spec](/docs/formatting). You
can specify values for `parse` and `link_names` to change formatting behavior.

The optional `attachments` argument should contain a JSON-encoded array of attachments.
For more information, see the [attachments spec](/docs/attachments).

By default links to media are unfurled, but links to text content are not. For
more information on the differences and how to control this, see the
[the unfurling documentation](/docs/unfurling).

## Authorship

By default, the `as_user` parameter is set to false and messages are posted as [bot_messages](/events/message/bot_message), with message authorship attributed to the default user name and icons associated with the [Custom Integration](/custom-integrations) or [Slack App](/slack-apps). 

With `as_user` set to false, you may also provide a `username` to explicitly specify the bot user's identity for this message, along with `icon_url` or `icon_emoji`.

Set `as_user` to `true` and the authenticated user will appear as the author of the message, ignoring any values provided for `username`, `icon_url`, and `icon_emoji`. Posting as the authenticated user **requires** the
`client` or `chat:write:user` [scopes](/docs/oauth#auth_scopes).

## Channels

You **must** specify a public channel, private group, or an IM channel with the `channel` argument. Each one behaves slightly differently based on the authenticated user's permissions and additional arguments:

#### Post to a public channel

You can either pass the channel's name (`#general`) or encoded ID (`C024BE91L`), and the message will be posted to that channel. The channel's ID can be retrieved through the [channels.list](/methods/channels.list) API method.

#### Post to a private group

As long as the authenticated user is a member of the private group, you can either pass the group's name (`secret-group`) or encoded ID (`G012AC86C`), and the message will be posted to that group. The private group's ID can be retrieved through the [groups.list](/methods/groups.list) API method.

#### Post to an IM channel

Posting to an IM channel is a little more complex depending on the value of `as_user`.

* If `as_user` is false:
    * Pass a username (`@chris`) as the value of `channel` to post to that user's @slackbot channel _as the bot_.
    * Pass the IM channel's ID (`D023BB3L2`) as the value of `channel` to post to that IM channel _as the bot_. The IM channel's ID can be retrieved through the [im.list](/methods/im.list) API method.
* If `as_user` is true:
    * Pass the IM channel's ID (`D023BB3L2`) as the value of `channel` to post to that IM channel _as the authenticated user_. The IM channel's ID can be retrieved through the [im.list](/methods/im.list) API method.

## Response

    {
        "ok": true,
        "ts": "1405895017.000506",
        "channel": "C024BE91L",
        "message": {
            ...
        }
    }

The response includes the timestamp (`ts`) and channel for the posted message. It also
includes the complete message object, as it was parsed by our servers. This
may differ from the provided arguments as our servers sanitize links,
attachments and other properties.

## Errors

{ERRORS}

## Warnings

{WARNINGS}
