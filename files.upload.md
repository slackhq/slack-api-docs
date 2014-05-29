
This method allows you to create or upload an existing file.


## Arguments

{ARGS}


The content of the file can either be posted using an `enctype` of `multipart/form-data` (with the file parameter named `file`), 
in the usual way that files are uploaded via the browser, or the content of the file can be sent as a POST var called `content`.
The latter should be used for creating a "file" from a long message/paste and forces "editbale" mode. 

In both cases, the type of data in the file will be intuited from the filename and the magic bytes in the file, for supported 
formats. Sending a `filetype` parameter will override this behavior (if a valid type is sent). Files uploaded via 
`multipart/form-data` will be stored either in hosted or editbale mode, based on certain heuristics (determined 
type, file size).

The file can also be shared directly into channels on upload, by specifying an optional argument `channels`. Channel IDs should
be comma separated if there is more than one.


## Response

The return value from the upload API call, assuming it's successful, is the standard file response (see [files.list](/methods/files.list)).

	{
	    "ok": true,
	    "file": {...}
	}

All newly-uploaded files are private, and only visible to the owner, until they are shared into a public channel (which could 
have happened at upload time via the `channels` argument).


## Errors

{ERRORS}
