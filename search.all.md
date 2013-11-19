
This method allows to to search both messages and files in a single call.


## Arguments

{ARGS}


## Response

The response returns matches broken down by their type of content, similar to the facebook/gmail auto-completed search widgets.

	{
	    "ok": true,
	    "query": "Best Pickles",
	    "messages": {...},
	    "files": {...}
	}

Within each content group, data is returned in the following format:

	{
	    "matches": [],
	    "paging": {
	        "count": 100,  - number of records per page
	        "total": 15,   - total records matching query
	        "page": 1,     - page of records returned
	        "pages": 1     - total pages matching query
	    }
	}

This block gives the (estimated) total number of matches of this type, then has an array containing the specified page of the 
top matches. The format of matches depends on the match type, as described in the documentation for
[search.messages](/methods/search.messages) and [search.files](/methods/search.files). These methods can be used to fetch
further pages of messages or files.


## Errors

{ERRORS}
