# mpim_joined event type

	{
		"type": "mpim_joined",
		"channel": {
			"is_mpim":true,
			'is_open':false,
			…
		}
	}

The `mpim_joined` event is sent to all connections for a user when that user
joins a multiparty DM. In addition to this message, `group_joined` and
`group_join` events will also be sent for backwards compatibility, since MPIMs
can also be treated as groups.  Clients that are MPIM aware can ignore all
`group_join` and `group_joined` events when the channel's `is_mpim` flag is
set to true.  MPIMs will always start closed for everyone but the creator.
