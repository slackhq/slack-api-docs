# team\_domain_change event type

	{
		"type": "team_domain_change",
		"url": "https://my.slack.com",
		"domain": "my"
	}

The `team_domain_change` event is sent to all connections for a team when the
team domain changes.

Since the existing domain will continue to work (causing a redirect) until it
is claimed by another team, clients don't need to do anything special with
this event. It is sent for the benefit of our web client, which needs to
reload when the domain changes.
