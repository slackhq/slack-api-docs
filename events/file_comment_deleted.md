# file_comment_deleted event

	{
		"type": "file_comment_deleted",
		"file": { … },
		"comment": "Fc67890"
	}

The `file_comment_deleted` event is sent when a file comment is deleted. It is
sent to all connected clients for users who can see the file. Clients can use
this notification to update comments in real-time for open files.

The `file` property is a [file object](/types/file).

Unlike [`file_comment_added`](/events/file_comment_added) and
[`file_comment_edited`](/events/file_comment_edited) the comment property only
contains the ID of the deleted comment, not the full comment object.
