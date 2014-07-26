# OAuth - User Authentication

OAuth2 is a protocol that lets external apps request authorization to private details
in a user's Slack account without getting their password.

Developers need to [register their application](/applications) before getting started. A registered OAuth 
application is assigned a unique Client ID and Client Secret. The Client Secret should not be shared.


## Web Authentication Flow

### Step 1 - Authorization

The authenticating web application should redirect users to the following URL:

    https://slack.com/oauth/authorize

The following values should be passed as GET parameters:

    client_id    - issued when you created your application (required)
    redirect_uri - URL to redirect back to (see below) (optional)
    scope        - permissions to request (see below) (optional)
    state        - unique string to be passed back upon completion
    team         - Slack team ID to restrict to (optional)

The `state` parameter should be used to avoid forgery attacks by passing in a value that's unique
to the user you're authenticating and checking it when auth completes.

If you don't pass a `team` param, the user will be allowed to choose which team they are 
authenticating against. Passing this param ensures the user will auth against an account on that
particular team.


### Step 2 - Token Issuing

If the user accepts your request, Slack redirects back to your site with a temporary code in a GET 
`code` parameter as well as the state you provided in the previous step in a `state` parameter.
If the states don't match, the request has been created by a third party and the process should be
aborted.

If all is well, exchange the code for an access token using the [`oauth.access`](/methods/oauth.access)
API method ([method documentation](/methods/oauth.access)).

    https://slack.com/api/oauth.access

    client_id     - issued when you created your application (required)
    client_secret - issued when you created your application (required)
    code          - the code param (required)
    redirect_uri  - must match the originally submitted URI (if one was sent)

The response JSON will contain an access token:

	{
		"access_token": "xoxt-23984754863-2348975623103",
		"scope": "read"
	}

You can then use this token to call protected API methods on behalf of the user.


### Step 2a - Denied Requests

If the user denies your request, Slack redirects back to your site with an `error` parameter.

    http://yourapp.com/oauth?
      error=access_denied

Applications should handle this condition appropriately.


## Auth Scopes

Scopes let you specify exactly what type of access you need. Scopes _limit_ access for 
OAuth tokens. They do not grant any additional permission beyond that which the user already has.

For the web flow, requested scopes will be displayed to the user on the authorize form.

Check headers to see what OAuth scopes you have, and what the API method accepts.

    $ curl https://slack.com/api/files.list?token=abcd -I
    HTTP/1.1 200 OK
    X-OAuth-Scopes: read, post
    X-Accepted-OAuth-Scopes: read

`X-OAuth-Scopes` lists the scopes your token has authorized.
`X-Accepted-OAuth-Scopes` lists the scopes that the action checks for.

The following scopes are available for Slack applications:

* __identify__ : Allows applications to confirm your identity.
* __read__ : Allows applications to read any messages and state that the user can see.
* __post__ : Allows applications to write messages and create content on behalf of the user.

NOTE: Your application can request the scopes in the initial redirection.
You can specify multiple scopes by separating them with a comma:

    https://slack.com/oauth/authorize?
      client_id=...&
      scope=read,post


## Redirect URIs

The `redirect_uri` parameter is optional. If left out, Slack will redirect users to the callback URL 
configured in the OAuth Application settings. If provided, the redirect URL's host and port must exactly 
match the callback URL. The redirect URL's path must reference a subdirectory of the callback URL.

    CALLBACK: http://example.com/path
    
    GOOD: https://example.com/path
    GOOD: http://example.com/path/subdir/other
    BAD:  http://example.com/bar
    BAD:  http://example.com/
    BAD:  http://example.com:8080/path
    BAD:  http://oauth.example.com:8080/path
    BAD:  http://example.org

