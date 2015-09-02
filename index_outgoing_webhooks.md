##Get data out of Slack in real-time.

Outgoing webhooks will run on messages sent to Slack when one or both of the following are true:

* The message is in the specified **channel**
* The message begins with one of the defined **trigger word(s)**

The [outgoing webhook integration](https://my.slack.com/services/new/outgoing-webhook) is only available in public channels. If you would like to get data out of private groups and DMs in real-time, try a [slash command](/slash-commands).


###Channel and/or Trigger

If a channel is **not** specified, then the trigger word(s) are required -- otherwise, the trigger word(s) are optional.

If both are specified, then the message must match both conditions.

###POST Data

When a chat message is received that matches the conditions, a POST will be sent to all of the URLs defined like so:

    token=XXXXXXXXXXXXXXXXXX
    team_id=T0001
    team_domain=example
    channel_id=C2147483705
    channel_name=test
    timestamp=1355517523.000005
    user_id=U2147483697
    user_name=Steve
    text=googlebot: What is the air-speed velocity of an unladen swallow?
    trigger_word=googlebot:

Please note that the content of [message attachments](/docs/attachments) will not be included in the outgoing POST data.

###Responding

If the handler wishes to post a response back into the channel, the following JSON should be returned as the body of the response:

    {
      "text": "African or European?"
    }

Empty bodies or bodies with an empty `text` property will simply be ignored. Non-200 responses will be retried a reasonable number of times.

Responses will be posted using the bot name and icon configured in the integration. However, if you would like to change the name on a per-response basis, simply include the `username` parameter in your response.
