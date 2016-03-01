
This method allows you to create or upload an existing file.


## Arguments

{ARGS}


The content of the file can either be posted using an `enctype` of `multipart/form-data` (with the file parameter named `file`), 
in the usual way that files are uploaded via the browser, or the content of the file can be sent as a POST var called `content`.
The latter should be used for creating a "file" from a long message/paste and forces "editable" mode.

In both cases, the type of data in the file will be intuited from the filename and the magic bytes in the file, for supported 
formats. 

Sending a valid `filetype` parameter will override this behavior. Possible `filetype` values can be found in the [`file` object definition](/types/file#file_types).

Files uploaded via 
`multipart/form-data` will be stored either in hosted or editable mode, based on certain heuristics (determined
type, file size).

The file can also be shared directly into channels on upload, by specifying an optional argument `channels`. If there's more than one channel name or ID in the `channels` string, they should be comma-separated.


## Response

If successful, the response will include a [file object](/types/file).

	{
	    "ok": true,
	    "file": {...}
	}

By default all newly-uploaded files are private and only visible to the owner.
They become public once they are shared into a public channel (which can
happen at upload time via the `channels` argument).

## Examples

Upload "dramacat.gif" and share it in channel, using `multipart/form-data`:

	curl -F file=@dramacat.gif -F channels=C024BE91L,#general -F token=xxxx-xxxxxxxxx-xxxx https://slack.com/api/files.upload

Create an editable file containing the text "Hello":

	curl -F content="Hello" -F token=xxxx-xxxxxxxxx-xxxx https://slack.com/api/files.upload


## Errors

{ERRORS}

## Warnings

{WARNINGS}
