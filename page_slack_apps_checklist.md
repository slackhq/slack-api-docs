# Slack App Directory Checklist

We review [Slack Apps](/slack-apps) submitted to the [App Directory](https://slack.com/apps).

Follow this guide to help your app go through the review process quickly and smoothly. We've highlighted the most important elements for your app listing.

This guide does not replace or supersede our [Developer Policy](/developer-policy), which must be adhered to at all times. The Developer Policy is listed here [https://api.slack.com/developer-policy](https://api.slack.com/developer-policy).

## Technical

### Appropriate Scopes:
* Your app only uses scopes that it needs to work.
* If you're still using the `read` or `post` scopes, or you use scopes that access more than your app requires, we'll ask you to change them before your app is accepted to the App Directory. You can find our [granular scopes](/docs/oauth-scopes) here: [https://api.slack.com/docs/oauth-scopes](https://api.slack.com/docs/oauth-scopes).

### Slack Button:
* Display the `Add To Slack` button for users to install your app from your site.

## Listing

### Appropriate name
* Your app's name should not infringe upon a trademark or copyright for any other products or services. Also, if you have any reference to Slack or Slackbot in the app name, we will ask you to remove it. You can find our [brand guidelines](https://slack.com/brand-guidelines) here: [https://slack.com/brand-guidelines](https://slack.com/brand-guidelines)

### Good Icon:
* Your app has a high quality, distinctive icon: a 512px by 512px or larger image is required.
* Icons cannot infringe on anyone else's copyright or trademark. If your icon resembles Slackbot or has the Slack icon within it we will ask you to change it.

### Short description:
* 10 words or less, clear and concise.

### Long description:
* Your app has a well written, detailed description of what it does.
* A great description would include information about your service in general as well as your Slack integration. It can contain simple Markdown (bold, italics, `code`) and can contain line breaks to display the information more clearly.

### Installation link:
* This is how customers install your app, so it's important to make it great. Think of this as the landing page for your app.
    * Information about your services
    * Information about how the app interacts with Slack
    * A clearly visible "[Add to Slack](/docs/slack-button)" button as soon as the user opens the page
    * If your "Add to Slack" button is behind a login page, make sure you have clear instructions about how to access that button after creating an account/logging in.
* Good examples: [https://foursquare.com/apps/slack](https://foursquare.com/apps/slack), [http://ideabot.co/ideas](http://ideabot.co/ideas)

### Customer support link
* As part of your submission to the App Directory, you agree to "Keep your App updated and your support channel active" so please ensure that the link you provide is to an active and responsive support channel.

### Customer support email
* Please make sure this is an email address that you check regularly and is clearly connected to your app.

### Privacy policy link
* Your app has a posted privacy policy, which will be linked from the app's directory listing. Even if all you store from a team is their token during the OAuth process, this must be spelled out and available for the user to read before they install your app.

## User Experience

### Formatting
* Messages within Slack should be [clearly formatted](/docs/formatting) so that users can see the information clearly. If your app isn't already taking advantage of the formatting and attachment information, see [https://api.slack.com/docs/formatting](https://api.slack.com/docs/formatting), to improve your app's messages.

### Spelling & Language
* Make sure that messages from your app within Slack don't contain any typos or grammatical errors which result in a confusing experience for the user.

### Your app or bot icon
* Just like your app's icon in the App Directory, your app or bot's icon within Slack should be clear and distinctive so that it can easily be distinguished from other users and bots.
