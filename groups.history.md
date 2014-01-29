
This method returns a portion of messages/events from the specified private group.
To read the entire history for a group, call the method with no `latest` or 
`oldest` arguments, and then continue paging using the instructions below.


## Arguments

{ARGS}


## Response

	{
	    "ok": true,
	    "latest": "1358547726.000003",
	    "messages": [
	        {
	            "type": "message",
	            "ts": "1358546515.000008",
	            "user": "U2147483896",
	            "text": "Hello"
	        },
	        {
	            "type": "message",
	            "ts": "1358546515.000007",
	            "user": "U2147483896",
	            "text": "World",
	            "is_starred": true,
	        },
	        {
	            "type": "something_else",
	            "ts": "1358546515.000007",
	            "wibblr": true
	        }
	    ],
	    "has_more": false
	}


The `latest` and `oldest` timestamps (if specified as arguments) are returned, along
with the most recent 100 messages from between (not inclusive) the two timestamps. If there were more than
100 messages between those two points, then `has_more` will be true. In this case, a client can 
make another call, using the `ts` value of the final message as the `latest` param,
to get the next "page" of messages. The `is_limited` boolean is only included for free teams that have
reached the free message limit. If true, there are messages before the current result set, but they
are beyond the message limit.

Messages of type `"message"` are user-entered text messages sent to the group, while other types
are events that happened within the group. All messages have both a `type` and a sortable
`ts`, but the other fields depend on the `type`. For a list of all possible events,
see the [channel messages](/docs/messages) documentation.

If a message has been starred by the calling user, the `is_starred` property will be present and
true. This property is only added for starred items, so is not present in the majority of messages.


# Errors

{ERRORS}
