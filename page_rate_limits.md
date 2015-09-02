# Rate limits

The Slack API and all integrations are subject to rate limiting.

## Message Posting

In general we allow applications that integrate with Slack to send no more than one message per second. We allow bursts over that limit for short periods. However, if your app continues to exceed the limit over a longer period of time it will be rate limited.

If you go over these limits when using our HTTP based APIs, including Incoming Webhooks, Slack will start returning a `HTTP 429 Too Many Requests` error, a JSON object containing the number of calls you have been making, and a `Retry-After` header containing the number of seconds until you can retry.

If you go over these limits when using our [Real Time Messaging API](/rtm) you will receive an error message as a reply. If you continue to send messages your application will be disconnected.

Continuing to send messages after being rate limited runs the risk of having your application permanently disabled.

These limits exist because Slack is primarily a communication tool for humans. Our goal is to detect applications that may be unintentionally spammy and quiet them down to avoid hindering a team’s ability to communicate and use their archive.

Other services provide a better interface for logging, searching, aggregating and archiving on messages that occur at higher volumes. These include [Papertrail](https://papertrailapp.com/) (which [integrates directly with Slack](https://my.slack.com/services/new/papertrail)), [Logentries](https://logentries.com/) (also [integrates with Slack](https://my.slack.com/services/new/logentries)), [Loggly](https://www.loggly.com/), [Splunk](http://www.splunk.com/) and [LogStash](http://logstash.net/).

## Other functionality

We reserve the right to rate limit other functionality to prevent abuse, spam, denial-of-service attacks, or other security issues. Where possible we'll return a descriptive error message, but the nature of this type of rate limiting often prevents us from providing more information.
