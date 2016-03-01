<img src="/img/api/homepage_slack_apps-2x.png" class="getting_started_icon" alt="Building Slack apps" />
So you want to build an app that other Slack teams can use. Well, you've come to the right place. Slack apps can bundle several of our [custom integration](/custom-integrations) tools ([incoming webhooks](/incoming-webhooks), [bot users](/bot-users) and [slash commands](/slash-commands) built for your team) into an easy-to-install application.

You can specify your app's [required permissions](/docs/oauth-scopes#app-scopes) and users installing the app may review these permissions and configure settings right within our OAuth-based [authentication flow](/docs/oauth).

Once you've built your app, you can submit it to our [App Directory](https://slack.com/apps). Our team will review your submission and work with you to get it listed. Of course, you'll want to add a [Slack Button](/docs/slack-button) to your website to make installation easy for your users.

Let's walk through what it takes to build a Slack app.

1. [Decide which APIs your app needs](#what-it-does)
2. [Create a Slack app and bundle together your integration points](#create-app)
4. [Setup your "Add to Slack" Button](#slack-button)
5. [Add your application to the directory](#directory)

---

## <a name="what-it-does"></a> What do you want your Slack app to do?

You know you want to build a Slack app, but which platform features do you need to get there?

Start by building a [custom integration](/custom-integrations) for your own team on Slack. If you don't have a team or just want your own personal sandbox to develop in, [create a new team](https://slack.com/create).

Once you're ready to share your app with the world, you can easily convert a collection of custom integrations in to a packaged Slack app.

You will be able to combine the following custom integration tools into a bundled app:

* **Send data into Slack with Incoming Webhooks**

	Incoming webhooks are the simplest way to automatically post messages from your service into Slack.

	You can prototype this behavior using custom [incoming webhooks](/incoming-webhooks), and easily transition to an app when you're ready. Once you have created an app and a team has authenticated it, you will receive a payload containing the Webhook URL, which you can use to send notifications straight into Slack.

	**Note:** As a Slack app, you will not be able to set all of the message parameters available in custom integrations. `channel` will always correspond to the channel selected by the team member installing your application, while the `username`, `icon_url`, and `icon_emoji` values will inherit the options you've already configured in your application record.

	Read the full [incoming webhook documentation](/incoming-webhooks).


* **Invoke actions outside of Slack with Commands**

	Commands can be used to trigger an external service action, or to request an on-demand update. You can prototype your app command using custom [slash commands](/slash-commands). Later, when setting up or editing your Slack app, you can attach one or more commands to your app.

	**Note:** App commands can only be sent to your externally hosted server as POST and GET requests over HTTPS. Valid certificates are required, and they cannot be self-signed.

	Read the full [slash command documentation](/slash-commands).


* **Build a bot user**

	Bot users connect to Slack in [real-time via websockets](/rtm), allowing users to converse with them just like they would with another human user. You can prototype your real-time bot with a custom [bot user](/bot-users) integration. When creating or editing your Slack app, you'll be asked to choose a suggested username for the bot, which should correspond with the name of your app.

	Read the full [bot user documentation](/bot-users).



* **Use Advanced APIs**

	If needed, your app can request additional permissions to make calls to the [Web API](/web). Review how [OAuth scopes correspond to API methods](/docs/oauth-scopes) to determine the minimum permissions that you need.

	Read the full [Web API](/web) and [RTM API](/rtm) documentation.



---

## <a name="create-app"></a> Create an app

When you're ready to turn your custom integration into an app, you'll first need to [create your Slack app](/applications/new). You must be logged in to a Slack account to do this, as the application record will be connected to this account. You'll be asked to fill out some basic information (name, description, icon) and will be given a `client_id` and `client_secret` that you will use in your OAuth client.

You can also add commands and a bot user to your Slack app at this point. These will be installed on a user's team once they authenticate your app.

<a href="/applications/new" class="btn header_btn">Create your Slack app</a>

---


## <a name="permissions"></a> Determine the permissions that your app needs

We provide a wide range of granular scopes that allow you to request the exact permissions that your app needs. For example, if you only need to post updates to a channel once an hour, you should only request the `incoming-webhook` scope. The [full inventory of scopes](/docs/oauth-scopes) list the API methods that each scope corresponds to. Here are some examples:

* With the `reactions:read` and `emoji:read` scopes, your app can use related API methods to build a leaderboard of team members' reactions.
* By requesting the `incoming-webhook` scope, users can grant your app access to post messages to a Slack channel of their choice, just like a custom incoming webhook integration.
* By requesting the `commands` scope, authenticated users will have access to any commands that you have configured in your app.
* By requesting the `bots` scope, you will receive a bot user token upon completion of an OAuth flow. You can use this bot user token to connect to the [Real Time Messaging API](/rtm).
* By requesting other granular object scopes, like `channels:read` or `files:write`, you will be able to call their corresponding Web API methods.

See [Slack app scopes](/docs/oauth-scopes#app-scopes) for more information on `incoming-webhook`, `commands`, and `bots` scopes.

---

## <a name="slack-button"></a> Set up an "Add to Slack" button

The simplest way for teams to install Slack apps is with an "Add to Slack" button.

Use [this handy button code widget](/docs/slack-button#button-widget) to choose your Slack app and select the scopes that you need. The widget generates some HTML code that you can use to add the "Add to Slack" button on your site.

If you'd prefer to use your own button or link, you can simply use the OAuth URL generated by the widget.

---

## <a name="directory"></a> Add your app to our Directory

When you're ready to publish your app, you can submit it to be reviewed and added to [our directory](https://slack.com/apps). Apps should be easy for teams to install and use. Our application review team will install and use your application and follow up with you for more details. As we get many submissions, there may be a short delay.

We recommend following our [Slack App Directory Checklist](/docs/slack-apps-checklist) before submitting your app for inclusion.

Additionally, please review our [API Terms of Service](https://slack.com/terms-of-service/api), [Brand Guidelines](https://slack.com/brand-guidelines), and [Slack App Developer Policy](/developer-policy).

<a href="https://airtable.com/shrBP6blw8I7bOYN0" class="btn header_btn">Submit your app here!</a>
