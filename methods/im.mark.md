
This method moves the read cursor in a direct message channel.


## Arguments

{ARGS}


## Response

	{
		"ok": true
	}

After making this call, the mark is saved to the database and broadcast via the message server to
all open connections for the calling user.

Clients should try to avoid making this call too often. When needing to mark a read position, a client
should set a timer before making the call. In this way, any further updates needed during the timeout
will not generate extra calls (just one per channel). This is useful for when reading scroll-back history,
or following a busy live channel. A timeout of 5 seconds is a good starting point. Be sure to flush these
calls on shutdown/logout.


## Errors

{ERRORS}

## Warnings

{WARNINGS}
