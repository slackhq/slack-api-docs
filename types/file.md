# File Objects

A file object contains information about a file shared with a team.

	{
	    "id" : "F2147483862",
	    "created" : 1356032811,
	    "timestamp" : 1356032811,

	    "name" : "file.htm",
	    "title" : "My HTML file",
	    "mimetype" : "text\/plain",
	    "filetype" : "text",
	    "pretty_type": "Text",
	    "user" : "U2147483697",

	    "mode" : "hosted",
	    "editable" : true,
	    "is_external": false,
	    "external_type": "",

	    "size" : 12345,

	    "url": "https:\/\/slack-files.com\/files-pub\/T024BE7LD-F024BERPE-09acb6\/1.png",
	    "url_download": "https:\/\/slack-files.com\/files-pub\/T024BE7LD-F024BERPE-09acb6\/download\/1.png",
	    "url_private": "https:\/\/slack.com\/files-pri\/T024BE7LD-F024BERPE\/1.png",
	    "url_private_download": "https:\/\/slack.com\/files-pri\/T024BE7LD-F024BERPE\/download\/1.png",

	    "thumb_64": "https:\/\/slack-files.com\/files-tmb\/T024BE7LD-F024BERPE-c66246\/1_64.png",
	    "thumb_80": "https:\/\/slack-files.com\/files-tmb\/T024BE7LD-F024BERPE-c66246\/1_80.png",
	    "thumb_360": "https:\/\/slack-files.com\/files-tmb\/T024BE7LD-F024BERPE-c66246\/1_360.png",
	    "thumb_360_gif": "https:\/\/slack-files.com\/files-tmb\/T024BE7LD-F024BERPE-c66246\/1_360.gif",
	    "thumb_360_w": 100,
	    "thumb_360_h": 100,

	    "permalink" : "https:\/\/tinyspeck.slack.com\/files\/cal\/F024BERPE\/1.png",
	    "edit_link" : "https:\/\/tinyspeck.slack.com\/files\/cal\/F024BERPE\/1.png/edit",
	    "preview" : "&lt;!DOCTYPE html&gt;\n&lt;html&gt;\n&lt;meta charset='utf-8'&gt;",
	    "preview_highlight" : "&lt;div class=\"sssh-code\"&gt;&lt;div class=\"sssh-line\"&gt;&lt;pre&gt;&lt;!DOCTYPE html…",
	    "lines" : 123,
	    "lines_more": 118,

	    "is_public": true,
	    "public_url_shared": false,
	    "channels": ["C024BE7LT", …],
	    "groups": ["G12345", …],
	    "ims": ["D12345", …],
	    "initial_comment": {…},
	    "num_stars": 7,
	    "is_starred": true,
	    "pinned_to": ["C024BE7LT", …],
	    "reactions": [
		{
			"name": "astonished",
			"count": 3,
			"users": [ "U1", "U2", "U3" ]
		},
		{
			"name": "facepalm",
			"count": 1034,
			"users": [ "U1", "U2", "U3", "U4", "U5" ]
		}
	    ]
	}

The `name` parameter may be `null` for unnamed files.

The `created` property is a unix timestamp representing when the file was
created. The `timestamp` property contains the same data as `created`, but is
deprecated and is provided only for backwards compatibility with older clients.

The `mimetype` and `filetype` props do not have a 1-to-1 mapping, as multiple different files types ('html', 'js',
etc.) share the same mime type. The `pretty_type` property contains a human-readable version of the type.

The `mode` property contains one of `hosted`, `external`, `snippet` or `post`.
The `editable` property indicates that files are stored in editable mode. The `is_external` property indicates
whether the master copy of a file is stored within the system or not. If the file `is_external`, then the `url`
property will point to the externally-hosted master file. Further, the `external_type` property will indicate what
kind of external file it is, e.g. `dropbox` or `gdoc`.

The `url` property points to a publically sharable URL directly to the file contents.
Only editable-mode files currently have a `url_download` parameter. This URL includes headers which force a browser
download. The `size` parameter is the filesize in bytes. The `url_private` and `url_private_download` props
are the same, but require cookie auth to access. These URLs should be used by the web client, but can be ignored
by other clients.

If a thumbnail is available for the file, the URL to a 64x64 pixel will be returned as the `thumb_64` prop.
The `thumb_80` prop (when present) contains the URL of an 80x80 thumb. Unlike the 64px thumb, this size is
guaranteed to be 80x80, even when the source image was smaller (it's padded with transparent pixels).
A variable sized thumb will be returned as `thumb_360`, with its longest size no bigger than 360 (although
it might be smaller depending on the source size). Dimensions for this thumb are returned in `thumb_360_w`
and `thumb_360_h`. In the case where the original image was an animated gif with dimensions greater than 360
pixels, we also created an animated thumbnail and pass it as `thumb_360_gif`.

The `permalink` URL points to a single page for the file containing details, comments and a download link.
The `edit_link` is only present for posts and snippets and is the page at which the file can be edited.

For posts, we also include a short plain-text `preview` than can be shown in place of a tumbnail.

For snippets, we include a simple `preview` of the contents (a few truncated lines of plaintext), as well as a
more complex syntaxed highlighted preview (`preview_highlight`) in HTML. The total count of lines in the snippet
if returned in `lines`, while `lines_more` contains a count of lines not shown in the preview.

If a file is public, the `is_public` flag will be set.

If a file's public URL has been shared, the `public_url_shared` flag will be set.

The `channels` array contains the IDs of any channels into which the file is currently shared. The `groups` array
is the same but for private groups. Groups are only returned if the caller is a member of that group. Finally, the
`ims` array is the same but for IM channels. IMs are only returned if the caller is a member of that IM channel.

The `num_stars` property contains the number of users who have starred this file. It is not present if no users
have starred it. The `is_starred` property is present and true if the calling user has starred the file, else
it is omitted.

The `pinned_to` array contains the IDs of any channels to which the file is currently pinned.

The `reactions` property contains any reactions that have been added to the file and gives information about the
type of reaction, the total number of users who added that reaction and a (possibly incomplete) list of users who have
added that reaction to the file. The users array in the `reactions` property might not always contain all users
that have reacted (we limit it to X users, and X might change), however `count` will always represent the count of all
users who made that reaction (i.e. it may be greater than `users.length`). If the authenticated user has a given reaction
then they are guaranteed to appear in the `users` array, regardless of whether `count` is greater than `users.length` or not.

The `initial_comment` will be a comment from the file uploader, and will only be set when the uploader commented on the file at the
time of upload. Clients can use this to display the comment with the file when announcing new file uploads.
