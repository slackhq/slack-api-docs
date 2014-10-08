
This method posts a message to a channel.


## Arguments

{ARGS}

## Formatting

Messages are formatted as described in the [formatting spec](/docs/formatting). You
can specify values for `parse` and `link_names` to change formatting behavior.

The optional `attachments` argument should contain a JSON-encoded array of attachments.
For more information, see the [attachments spec](/docs/attachments).

By default links to media are unfurled, but links to text content are not. For
more information on the differences and how to control this, see the
[the unfurling documentation](/docs/unfurling).

## Response

	{
		"ok": true,
		"ts": "1405895017.000506"
		"channel": "C024BE91L"
	}

## Errors

{ERRORS}
