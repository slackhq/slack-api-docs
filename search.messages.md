
This method returns messages matching a search query.


## Arguments

{ARGS}


## Response

The response envelope contains paging and result information:

	{
	    "ok": true,
	    "query": "test",
	    "messages": {
	        "total": 829,
	        "paging": {
	            "count": 20,
	            "total": 829,
	            "page": 1,
	            "pages": 42
	        },
	        "matches": [
	            {...},
	            {...},
	            {...}
	        ]
	    }
	}

The actual matches are returned as hashes containing contextual messages:

	{
	    "type": "message",
	    "channel": {
	        "id": "C2147483753",
	        "name": "foo"
	    },
	    "user": "U2147483709",
	    "username": "johnnytest",
	    "ts": "1359414002.000003",
	    "text": "mention test: johnnyrodgers".
	    "permalink": "https:\/\/example.slack.com\/channels\/foo\/p1359414002000003",
	    "previous_2": {
	        "user": "U2147483709",
	        "username": "johnnytest",
	        "text": "This was said before before",
	        "ts": "1359413987.000000",
	        "type": "message"
	    },
	    "previous": {
	        "user": "U2147483709",
	        "username": "johnnytest",
	        "text": "This was said before",
	        "ts": "1359414001.000000",
	        "type": "message"
	    },
	    "next": {
	        "user": "U2147483709",
	        "username": "johnnytest",
	        "text": "This was said after",
	        "ts": "1359414020.000000",
	        "type": "message"
	    },
	    "next_2": {
	        "user": "U2147483709",
	        "username": "johnnytest",
	        "text": "This was said after after",
	        "ts": "1359414021.000000",
	        "type": "message"
	    }
	}

Messages are searched primarily inside the message text themselves, with a lower priority on the messages 
immediately before and after. If more than one search term is provided, user and channel are also matched 
at a lower priority. To specifically search within a channel, group, or DM, add `in:channel_name`, 
`in:group_name`, or `in:username`. To search for messages from a specific speaker, add `from:username` or 
`from:botname`.

For IM results, the `type` is set to `"im"` and the `channel.name` property contains the user ID of the 
target user. For private group results, type is set to `"group"`.

To further expand the context around a result, see the [search.context](/methods/search.context) method.

All search methods support the `highlight` parameter. If specified, the matching query terms will be marked 
up in the results so that clients may replace them with appropriate highlighting markers
(e.g. `<span class="highlight"></span>`). The UTF-8 markers we use are:

	start: "\xEE\x80\x80"; # U+E000 (private-use)
	end  : "\xEE\x80\x81"; # U+E001 (private-use)


## Errors

{ERRORS}
