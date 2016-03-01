This method lists the integration activity logs for a team, including when integrations are added, modified and removed. This method can only be called by Admins.

## Arguments

{ARGS}


## Response

The response contains a list of activity logs followed by pagination
information.

	{
		"ok": true,
		"logs": [
			{
				"service_id": "1234567890",
				"service_type": "Google Calendar",
				"user_id": "U1234ABCD",
				"user_name": "Johnny",
				"channel": "C1234567890",
				"date": "1392163200",
				"change_type": "enabled",
				"scope": "incoming-webhook"
			},
			{
				"app_id": "2345678901",
				"app_type": "Johnny App"
				"user_id": "U2345BCDE",
				"user_name": "Billy",
				"date": "1392163201",
				"change_type": "added"
				"scope": "chat:write:user,channels:read"
			},
			{
				"service_id": "3456789012",
				"service_type": "Airbrake",
				"user_id": "U3456CDEF",
				"user_name": "Joey",
				"channel": "C1234567890",
				"date": "1392163202",
				"change_type": "disabled",
				"reason": "user",
				"scope": "incoming-webhook"
			},
			"paging": {
				"count": 3,
				"total": 3,
				"page": 1,
				"pages": 1
			}
		]
	}

Logs can contain data for either a service or API application. If it's a service, `service_id` and `service_type` will be returned, and if it's an API application, `app_id` and `app_type` will be returned.

Logs can also contain different `change_types`. The possible types are: `added`, `removed`, `enabled`, `disabled`, and `updated`.

If the log entry is an RSS feed, the log will also contain `rss_feed` (with a value of `true`), `rss_feed_change_type`, `rss_feed_title` and `rss_feed_url`.

When a `disabled` event is logged, its log entry will also contain a `reason` for why the event occurred. The list of possible reasons are:

* `user` - Manually disabled by user
* `rate_limits` - Rate limits exceeded
* `slack` - Disabled by Slack
* `errors` - Too many errors
* `system` - A system change (i.e. channel archived)
* `admin` - Admin (i.e. user deleted)
* `api_decline` - User declied the API TOS
* `deauth` - Service deauthorized

The paging information contains the `count` of logs returned, the `total` number of logs, the `page` of results returned in this response and the total number of `pages` available.

## Errors

{ERRORS}

## Warnings

{WARNINGS}
