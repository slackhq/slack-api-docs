
The Slack API is made up of several different tools that enable you to build different kinds of Slack apps. In this guide, we'll cover the most common scenarios that products and services are building with Slack APIs. We'll also offer our best advice about how to save a bit of time and build the best possible Slack app for your needs.

---

## Which API tools should I use?

Well, it depends! Our API tools let you extend Slack to play nicely with your team's workflow, external services, and other applications. But how do you figure out where to start, and which Slack APIs are best for you? You've come to the right place. Let us guide you through some examples that will help you pick the right tools for each job.

### I run a service and want the simplest way for my users to integrate it with Slack.

Maybe you run a newsletter service that sends notifications to publishers when a new person signs up for their mailing list. 

Or you're an e-commerce service and want to let your users get summaries of sales from their online store, either automatically or on demand. 

Whatever kind of service you run: You want people to know the things they need to know, as quickly, and as easily, as possible. And the Slack button wants to help you out with that.

<img src="/img/add_to_slack_promo.png" style="float:right;margin:0 0 10px 10px;border:0;">

**Best way to do this:** Use the [Slack button](https://api.slack.com/docs/slack-button). The new Slack button is the simplest way to offer your service to teams using Slack. A Slack button app gives you [incoming webhooks](https://api.slack.com/incoming-webhooks) and [slash commands](https://api.slack.com/slash-commands) wrapped in OAuth. You write the commands and the webhook that your app needs, and configure the options for your users. Then your users can install it in just a few clicks. Over the next few months, we'll be expanding the capabilities of apps that can be added via the Slack button, so now is a great time to get started with them! [Read more about how to implement the Slack button on your site](https://api.slack.com/docs/slack-button).

![Screenshot of incoming webhook message](/img/api/guide_breaking_news_screenshot.png)

### I want to post custom messages, links, images, and other content in my Slack team from other systems

Like most businesses today, you probably use multiple systems to keep things running, and they all have information you need throughout the day. Not all of those systems will have pre-built Slack integrations, and of the ones that do, they might not deliver the specific information that your team needs. In this case, you will need to create something for yourself.

Best way to do this as a custom feature for your team: With an [incoming webhook](https://api.slack.com/incoming-webhooks). They're the simplest way to programmatically send messages into Slack. Simply send a JSON payload containing your message content to a pre-configured incoming webhook URL that your users set up for you, and Slack will turn it into a message for the right team, in the right channel. For more information and some examples, read our [incoming webhook documentation](https://api.slack.com/incoming-webhooks).

![Screenshot of messages posted via incoming webhooks](/img/api/guide_incoming_webhook.png)

### I want to enable users to interact with my product _from Slack_

Let's say you have a dictionary tool, or a bug tracker, or a task management app, and you'd like your users to interact with it from within Slack. 

For example, you'd like a way for users to type `/todo list` to get a list of tasks assigned to them, or `/todo add Finish writing API guide` to create a new task for themselves. Throw in a username to assign the task to one of your teammates — `/todo for @mattMake some graphics for the API guide`.

**Best way to do this:** Set up a [slash command](/slash-commands). This will let your users make queries or trigger external actions right from within Slack.

![Screenshot of a slash command](/img/api/guide_slash_command.png)

### I want to build a real-time conversational bot

Lots of people are very excited about building bots these days. Bots allow you to create a conversational interface with any external service. It's not easy, but it's fun. To do this, [create a bot user](/bot-users) to connect to Slack and post messages, along with many [other APIs](/bot-users#method_list).

![Screenshot of a bot discussion](/img/api/guide_bot_user.png)

---

## Get news about future API updates

These are just a few of the many different kinds of apps that you can build on top of Slack. For more ideas, follow [@SlackAPI](https://twitter.com/slackapi) on Twitter or read our collection of [Slack App-related articles on Flipboard](https://flipboard.com/@slackapi/several-people-are-coding%E2%80%A6-ktn2udc3y).

To learn about future enhancements to our APIs, [register as an API developer](https://api.slack.com/register), tell us a bit about yourself and the things you'd like to build, and we'll make sure you're the first to know about all the exciting things happening in the future.

<a href="https://api.slack.com/register" class="btn">Register as a Developer</a>

---

## Become an "official" integration

All of our [official integrations](https://slack.com/integrations) go through a review process, whether they were developed in-house or by the third-party service. This process is currently a bit bottlenecked on our side, as we can only work on a handful of new integrations at a time. The good news is that we're making some changes to our integration platform that will give developers the ability to better manage and distribute their integrations in Slack, and to let our team review and approve them more quickly.

In the meantime, we recommend exploring our API tools to determine the type of integration you would like to build. Once you've got the hang of things and validated that the integration is useful for you and your users on Slack, [tell us about your integration](https://slackhq.typeform.com/to/kOHQvo) and we'll add you to our queue.

If you have questions not covered by this guide, or there's anything else you'd like to let us know about, you can contact us at [integrations@slack.com](mailto:integrations@slack.com).

