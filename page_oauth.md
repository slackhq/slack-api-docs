# Authenticating Users with OAuth

OAuth 2.0 is a protocol that lets your app request authorization to private details in a user's Slack account without getting their password.

You'll need to [register your app](/applications) before getting started. A registered app is assigned a unique Client ID and Client Secret which will be used in the OAuth flow. The Client Secret should not be shared.

The easiest way to enable teams to install your app is with the [Add to Slack](/docs/slack-button) button.

## The OAuth Flow

Slack uses OAuth 2.0's [authorization code grant flow](https://tools.ietf.org/html/rfc6749#section-4.1) to issue access tokens on behalf of users.

### Step 1 - Authorization

Your web or mobile app should redirect users to the following URL:

    https://slack.com/oauth/authorize

The following values should be passed as GET parameters:

    client_id    - issued when you created your app (required)
    scope        - permissions to request (see below) (required)
    redirect_uri - URL to redirect back to (see below) (optional)
    state        - unique string to be passed back upon completion (optional)
    team         - Slack team ID to restrict to (optional)

The `scope` parameter is a space-separated list of OAuth scopes, indicating which parts of the Slack user's account you'd like your app to be able to access. The complete list of scopes can be found [here](/docs/oauth-scopes).

The `state` parameter should be used to avoid forgery attacks by passing in a value that's unique to the user you're authenticating and checking it when auth completes.

If you don't pass a `team` param, the user will be allowed to choose which team they are authenticating against. Passing this parameter ensures the user will auth against a specific team.

For the best user experience, use the [Add to Slack](/docs/slack-button) button to direct users to the authorization step.

### Step 2 - Token Issuing

If the user authorizes your app, Slack will redirect back to your specified `redirect_uri` with a temporary code in a `code` GET parameter, as well as a `state` parameter if you provided one in the previous step. If the states don't match, the request may have been created by a third party and you should abort the process.

<p class="alert alert_info"><i class="ts_icon ts_icon_info_circle"></i> Authorization codes may only be exchanged once and expire 10 minutes after issuance.</p>

If all is well, exchange the authorization code for an access token using the [`oauth.access`](/methods/oauth.access) API method ([method documentation](/methods/oauth.access)).

    https://slack.com/api/oauth.access

    client_id     - issued when you created your app (required)
    client_secret - issued when you created your app (required)
    code          - the code param (required)
    redirect_uri  - must match the originally submitted URI (if one was sent)

You'll receive a JSON response containing an `access_token`:

	{
		"access_token": "xoxt-23984754863-2348975623103",
		"scope": "read"
	}

You can then use this token to call [API methods](/methods) on behalf of the user.

<p class="alert alert_info"><i class="ts_icon ts_icon_info_circle"></i> Please note that these access tokens do not expire.</p>

#### Bot user access tokens

If your Slack app includes a [bot user](/bot-users), upon approval the JSON response will contain an additional node containing an access token to be specifically used for your bot user, within the context of the approving team.

When you connect to [`rtm.start`](/methods/rtm.start) or use [Web API](/web) methods on behalf of your bot user, you should use this bot user access token instead of the top-level access token granted to your application.

Here's a more verbose example JSON response including a Bot user access token:

    {
        "access_token": "xoxp-XXXXXXXX-XXXXXXXX-XXXXX",
        "scope": "incoming-webhook,commands,bot",
        "team_name": "Team Installing Your Hook",
        "team_id": "XXXXXXXXXX",
        "incoming_webhook": {
            "url": "https://hooks.slack.com/TXXXXX/BXXXXX/XXXXXXXXXX",
            "channel": "#channel-it-will-post-to",
            "configuration_url": "https://teamname.slack.com/services/BXXXXX"
        },
        "bot":{
            "bot_user_id":"UTTTTTTTTTTR",
            "bot_access_token":"xoxb-XXXXXXXXXXXX-TTTTTTTTTTTTTT"
        }
    }

Within this response, the `bot` node contains two fields related to your bot user: `bot_user_id` and `bot_access_token`. Bot access tokens always begin with `xoxb`.

<p class="alert alert_warning"><i class="ts_icon ts_icon_warning"></i> <strong>Secure your bot user tokens</strong>, as with all tokens and credentials. Do not share tokens with users or anyone else. Bot user tokens have particularly expansive capabilities not afforded to typical user tokens issued on behalf of team members.</p>

### Step 2a - Denied Requests

If the user denies your request, Slack redirects back to your `redirect_uri` with an `error` parameter.

    http://yourapp.com/oauth?
      error=access_denied

Applications should handle this condition appropriately.

## Redirect URIs

The `redirect_uri` parameter is optional. If left out, Slack will redirect users to the callback URL configured in your app's settings. If provided, the redirect URL's host and port must exactly match the callback URL. The redirect URL's path must reference a subdirectory of the callback URL.

    CALLBACK: http://example.com/path

    GOOD: https://example.com/path
    GOOD: http://example.com/path/subdir/other
    BAD:  http://example.com/bar
    BAD:  http://example.com/
    BAD:  http://example.com:8080/path
    BAD:  http://oauth.example.com:8080/path
    BAD:  http://example.org

## Handling Multiple Authorizations

Your application may send a user through the OAuth flow multiple times.

You can utilize this behavior to re-verify a user's identity or to retrieve a user's access token again as needed. You can also use it to upgrade an access token's [OAuth scopes](/docs/oauth-scopes).

If your application _requires_ a basic set of permissions to function, but can utilize _optional_ permissions for advanced functionality, requesting additional scopes separately ensures that your application will have the access it needs to function without initially deterring users from approving it.

When your user is ready to indulge themselves in features requiring additional permissions, send them through the OAuth flow again, this time requesting the additional scopes you need.

For example, if your app uses Slack to sign in to your service, you may want to restrict your initial OAuth request to just the `identify` scope. If that same app also has an optional feature to import files from Slack using `files:read`, you can initiate the application approval process again, within context of the user's action, so they understand why the additional permissions are being requested.

This ensures that your app retains critical functionality (signing in to your app) without requiring optional permissions (access to the user's files) and also provides better context for the user.

### Appending Scopes

When you initially send a user through the OAuth flow, you receive a token that has the set of scopes you requested. Any subsequent time(s) you send that same user through the OAuth flow, any new scopes you request will be added to that initial set.

For example, if you initially request `identify channels:read` from a user, the initial token will have `identify channels:read`. If you send that same user through a second OAuth flow requesting `files:write`, the resulting token will have the new scope added to the previous set: `identify channels:read files:write`.

This process can be repeated any number of times, and each scope you request is **additive** to the scopes you've already been awarded. It is not possible to downgrade an access token's scopes.

As you make [Web API](/web) requests, a `X-OAuth-Scopes` HTTP header will be returned with every response indicating which scopes the calling token currently has:

    X-OAuth-Scopes: identify,channels:read,files:read,channels:write
