# Changelog

We improve the Slack platform every day by releasing new features, squashing bugs, and delivering fresh documentation. Here's an account of what's recently happened.


### February 2016
* <span class="btn btn_small pill_btn docs">Docs</span> Published this [changelog](/docs/changelog) you're reading right now. So that you can know about all this stuff. Tell your friends.
* <span class="btn btn_small pill_btn new_feature">APIs</span> New Web API methods: share files publicly with [`files.sharedPublicURL`](/methods/files.sharedPublicURL) or make them private again with [`files.revokePublicURL`](/methods/files.revokePublicURL).
* <span class="btn btn_small pill_btn new_feature">APIs</span> [`files.comments.add`](/methods/files.comments.add), [`files.comments.edit`](/methods/files.comments.edit), and [`files.comments.delete`](/methods/files.comments.delete) are now available to [bot users](/bot-users).
* <span class="btn btn_small pill_btn tools">Tools</span> Quickly find the right tools for your project with our new listing of [**often-used open source libraries**](/community).
* <span class="btn btn_small pill_btn tools">Tools</span> The handy [test token generator](/docs/oauth-test-tokens) previously found in the [Web API](/web) documentation now stands proud with its very own page.
* <span class="btn btn_small pill_btn docs">Docs</span> Need help? We have [some tips](/docs/support) for you.
* <span class="btn btn_small pill_btn docs">Docs</span> api.slack.com's sidebar is now better organized by topic.

### January 2016

* <span class="btn btn_small pill_btn deprecation">Alert</span> As of January 4th, 2016, authorization headers are now required for most Web API requests involving file URLs. See [this doc](/types/file#authentication) and [blog post](https://medium.com/slack-developer-blog/important-changes-to-files-in-the-web-api-eb38f2a9c1e7) for more information.
* <span class="btn btn_small pill_btn deprecation">Alert</span> `url` and `url_download` are no longer part of [file objects](/types/file)
* <span class="btn btn_small pill_btn docs">Docs</span> Enjoy our evolving collection of [**Frequently Asked Questions**](/faq) (and answers!)
* <span class="btn btn_small pill_btn new_feature">APIs</span> Responses to [Incoming Webhook](/incoming-webhooks) requests now include `channel_id`
* <span class="btn btn_small pill_btn new_feature">Apps</span> Make sure you're ready before submitting your Slack App for review by following this [**Slack App Checklist**](/docs/slack-apps-checklist).
* <span class="btn btn_small pill_btn docs">Docs</span> [Incoming Webhooks](/incoming-webhooks) documentation updated to better bait best practices and discourage fishy formatting behavior.
* <span class="btn btn_small pill_btn docs">Docs</span> The [file object](/types/file) documentation now includes a list of possible [file types](/types/file#file_types).

### December 2015

* <span class="btn btn_small pill_btn tools">Tools</span> Now you can upgrade your Slack App's [OAuth Scopes](/docs/oauth-scopes) by [**managing your apps**](/applications). [This article](https://medium.com/slack-developer-blog/how-to-upgrade-your-slack-oauth-scopes-96f1eb6e5bc8) explains it all.
* <span class="btn btn_small pill_btn new_feature">APIs</span> Don't press snooze until you've dreamed about our new [Do Not Disturb Web API](/methods#dnd) methods.
* <span class="btn btn_small pill_btn new_feature">Apps</span> You can now package [Bot Users](/bot-users) within [Slack Apps](/slack-apps), making your creations easier to distribute to teams.
* <span class="btn btn_small pill_btn new_feature">Apps</span> We launched the [Slack Application Directory](https://slack.com/apps), where teams can discover apps like yours.
* <span class="btn btn_small pill_btn new_feature">Apps</span> We [announced the Slack Fund](https://medium.com/slack-developer-blog/launch-platform-114754258b91) to "give developers the backing they need to build everything possible in Slack."
* <span class="btn btn_small pill_btn docs">Docs</span> The api.slack.com [home page](/) is fancier.
* <span class="btn btn_small pill_btn docs">Docs</span> Enjoy major updates to the [Slash Commands](/slash-commands) documentation, expanding on topics like... delayed responses.

### November 2015

* <span class="btn btn_small pill_btn deprecation">Alert</span> Announced [**important changes**](https://medium.com/slack-developer-blog/important-changes-to-files-in-the-web-api-eb38f2a9c1e7) to the Files methods of the Web API.
* <span class="btn btn_small pill_btn new_feature">APIs</span> Added [`team.integrationLogs`](/methods/team.integrationLogs) to the [Web API](/web).
* <span class="btn btn_small pill_btn new_feature">APIs</span> Added authorization support for thumbnail URLs appearing in [File objects](/types/file).
* <span class="btn btn_small pill_btn new_feature">Apps</span> More granular [OAuth scopes](/docs/oauth-scopes) are here! Now your apps can ask for the exact level of access you need.

Many wonderful developments occurred before November 2015, but they are not logged here.
