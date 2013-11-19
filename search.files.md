
This method returns files matching a search query.


## Arguments

{ARGS}


## Response

The response envelope contains paging and result information:

	{
	    "ok": true,
	    "query": "test",
	    "files": {
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

The actual matches are returned as hashes containing file information, in the same format used by
[files.list](/methods/files.list).

All search methods support the `highlight` parameter. If specified, the matching query terms will be marked 
up in the results so that clients may replace them with appropriate highlighting markers
(e.g. `<span class="highlight"></span>`). The UTF-8 markers we use are:

	start: "\xEE\x80\x80"; # U+E000 (private-use)
	end  : "\xEE\x80\x81"; # U+E001 (private-use)


## Errors

{ERRORS}
