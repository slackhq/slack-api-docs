##Easily control your Slackbot from external services

Slackbot is pretty awesome, but can't do everything. The Slackbot Remote integration fills in some of those gaps by letting you send messages to any channel as Slackbot.

Add a [Slackbot Remote integration](https://my.slack.com/services/new/slackbot) to get started.

##Sending messages

It's really easy to send messages as your team's Slackbot.

1. Set up a [Slackbot Remote integration](https://my.slack.com/services/new/slackbot). This will give you a Slackbot URL that is unique to your team.
2. Append the channel name to your URL like so: `&channel=%23general`
3. Send the text you would like Slackbot to say using HTTP POST. Send the text exactly as you would like it to appear as the body of your request. You can include our [standard message formatting](/docs/formatting/) in these messages, as well.

####Example

    curl --data "Hello from Slackbot" $'https://my.slack.com/services/hooks/slackbot?token=oLqLmTpxS5rDKghRQe5qbd9K&channel=%23general'

##Rate Limits

You can only send up to one message per second through Slackbot. Read our [rate limit documentation](/docs/rate-limits/) for more information.
