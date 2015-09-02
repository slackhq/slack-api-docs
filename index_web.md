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
error code.

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

Other properties are defined in the documentation for the relevant method.

## Authentication

API authentication is achieved via a bearer token which identifies a single
user. You can either use a generated full-access token (below), or register
your application with us and use [OAuth 2](/docs/oauth). If you plan to
authenticate several users, we strongly recommend using OAuth.

{TOKEN_LIST}

The auth token should be passed in all API calls as a parameter called `token`.
