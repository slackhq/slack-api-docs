
This method returns a list of files within the team. It can be filtered and sliced in various ways.


## Arguments

{ARGS}


## Response

	{
	    "ok": true,
	    "files": [
	        {...},
	        {...},
	        {...},
	        ...
	    ],
	    "paging": {
	        "count": 100,
	        "total": 295,
	        "page": 1,
	        "pages": 3
	    }
	}

The response contains a list of [file objects](/types/file), followed by paging information. Files are always returned with
the most recent first.

The paging information contains the `count` of files returned, the `total` number of
files matching the filter (if any was supplied), the `page` of results returned in this response and
the total number of `pages` available.

## Errors

{ERRORS}
