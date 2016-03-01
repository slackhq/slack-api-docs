# Slack Web API

The Slack Web API allows you to build applications that interact with Slack in
more complex ways than the integrations we provide out of the box.

## Basics

The Web API consists of [HTTP RPC-style methods](/methods), all of the form
`https://slack.com/api/METHOD`.

All methods must be called using HTTPS. Arguments can be passed as GET or
POST params, or a mix. The response contains a JSON object, which will always
contain a top-level boolean property `ok`, indicating success or failure. For
failure results, the `error` property will contain a short machine-readable
error code. In the case of problematic calls that could still be completed
successfully, `ok` will be `true` and the `warning` property will contain a
short machine-readable warning code (or comma-separated list of them, in the
case of multiple warnings).

```
{
    "ok": true,
    "stuff": "This is good"
}
```

```
{
    "ok": false,
    "error": "something_bad"
}
```

```
{
    "ok": true,
    "warning": "something_problematic",
    "stuff": "Your requested information"
}
```

Other properties are defined in the documentation for the relevant method.

## Authentication

Authenticate your Web API requests by providing a bearer token, which identifies a single user.

[Register your application](/applications) with Slack to obtain credentials for use with our [OAuth 2.0](/docs/oauth) implementation, which allows you to negotiate tokens on behalf of users and teams. Tokens should be passed in all Web API calls as a parameter called `token`.

While developing or testing your app, you may use test tokens using our [test token generator](/docs/oauth-test-tokens).

<p><a href="/docs/oauth-test-tokens" class="btn">Generate test tokens</a></p>

<p class="alert alert_warning"><i class="ts_icon ts_icon_warning"></i> <strong>Test tokens are just for you</strong>. Treat them as you would a password. Never share test tokens with other users or applications.</p>
