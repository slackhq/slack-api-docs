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
	    "username": "",
	    "size" : 12345,
	    "url_private": "https:\/\/slack.com\/files-pri\/T024BE7LD-F024BERPE\/1.png",
	    "url_private_download": "https:\/\/slack.com\/files-pri\/T024BE7LD-F024BERPE\/download\/1.png",
	    "thumb_64": "https:\/\/slack-files.com\/files-tmb\/T024BE7LD-F024BERPE-c66246\/1_64.png",
	    "thumb_80": "https:\/\/slack-files.com\/files-tmb\/T024BE7LD-F024BERPE-c66246\/1_80.png",
	    "thumb_360": "https:\/\/slack-files.com\/files-tmb\/T024BE7LD-F024BERPE-c66246\/1_360.png",
	    "thumb_360_gif": "https:\/\/slack-files.com\/files-tmb\/T024BE7LD-F024BERPE-c66246\/1_360.gif",
	    "thumb_360_w": 100,
	    "thumb_360_h": 100,
        "thumb_480": "https:\/\/slack-files.com\/files-tmb\/T024BE7LD-F024BERPE-c66246\/1_480.png",
        "thumb_480_w": 480,
        "thumb_480_h": 480,
        "thumb_160": "https:\/\/slack-files.com\/files-tmb\/T024BE7LD-F024BERPE-c66246\/1_160.png",
	    "permalink" : "https:\/\/tinyspeck.slack.com\/files\/cal\/F024BERPE\/1.png",
	    "permalink_public" : "https:\/\/tinyspeck.slack.com\/T024BE7LD-F024BERPE-3f9216b62c",
	    "edit_link" : "https:\/\/tinyspeck.slack.com\/files\/cal\/F024BERPE\/1.png/edit",
	    "preview" : "&lt;!DOCTYPE html&gt;\n&lt;html&gt;\n&lt;meta charset='utf-8'&gt;",
	    "preview_highlight" : &lt;div class=\"sssh-code\"&gt;&lt;div class=\"sssh-line\"&gt;&lt;pre&gt;&lt;!DOCTYPE html...",
	    "lines" : 123,
	    "lines_more": 118,
	    "is_public": true,
	    "public_url_shared": false,
	    "display_as_bot" : false,
	    "channels": ["C024BE7LT", ...],
	    "groups": ["G12345", ...],
	    "ims": ["D12345", ...],
	    "initial_comment": {...},
	    "num_stars": 7,
	    "is_starred": true,
	    "pinned_to": ["C024BE7LT", ...],
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
	    ],
	    "comments_count": 1
	}

## Basic fields

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

The `size` parameter is the filesize in bytes.

Depending on the file's `type`, you may encounter different fields relevant to that type. For instance, you may encounter fields such as `image_exif_rotation`, `original_w`, and `original_h` for images but not find those fields for HTML documents.

## Authentication

Authentication is **required** to retrieve file URLs.

The `url_private` property points to a URL to the file contents. Editable-mode files will also have a `url_private_download`
parameter, which includes headers to force a browser download. Both `url_private` and `url_private_download` require
an authorization header of the form:

    Authorization: Bearer A_VALID_TOKEN

In this case, `A_VALID_TOKEN` is representative of a real OAuth token, bearing at least the `files:read` scope. [Learn more about OAuth Scopes](/docs/oauth-scopes).

Fields providing URLs that require this form of authentication include:

* `url_private`
* `url_private_download`
* `thumb_64`
* `thumb_80`
* `thumb_160`
* `thumb_360`
* `thumb_480`
* `thumb_720`
* `thumb_960`
* `thumb_1024`

<p class="alert alert_info"><i class="ts_icon ts_icon_info_circle"></i> Please note that the <code>url</code> and <code>url_download</code> parameters have been deprecated. Please use <code>url_private</code> and <code>url_private_download</code> instead.</p>

## Thumbnails

If a thumbnail is available for the file, the URL to a 64x64 pixel will be returned as the `thumb_64` prop.

The `thumb_80` prop (when present) contains the URL of an 80x80 thumb. Unlike the 64px thumb, this size is
guaranteed to be 80x80, even when the source image was smaller (it's padded with transparent pixels).

A variable sized thumb will be returned as `thumb_360`, with its longest size no bigger than 360 (although it might be smaller depending on the source size). Dimensions for this thumb are returned in `thumb_360_w`
and `thumb_360_h`.

In the case where the original image was an animated gif with dimensions greater than 360 pixels, we also created an animated thumbnail and pass it as `thumb_360_gif`.

Depending on the original file's size, you may even find a `thumb_480`, `thumb_720`, `thumb_960`, or `thumb_1024` property.

All thumbnails **require** an
authorization header as described [above](#authentication).

## Permalinks

The `permalink` URL points to a single page for the file containing details, comments and a download link. If the file is available to the public, a `permalink_public` URL points to the public file itself.

The `edit_link` is only present for posts and snippets and is the page at which the file can be edited.

## Previews

For posts, we also include a short plain-text `preview` than can be shown in place of a thumbnail.

For snippets, we include a simple `preview` of the contents (a few truncated lines of plaintext), as well as a more complex syntax-highlighted preview (`preview_highlight`) in HTML. The total count of lines in the snippet
if returned in `lines`, while `lines_more` contains a count of lines not shown in the preview.

## Other fields

If a file is public, the `is_public` flag will be set.

If a file's public URL has been shared, the `public_url_shared` flag will be set.

The `channels` array contains the IDs of any channels into which the file is currently shared. The `groups` array is the same but for private groups. Groups are only returned if the caller is a member of that group. Finally, the
`ims` array is the same but for IM channels. IMs are only returned if the caller is a member of that IM channel.

The `num_stars` property contains the number of users who have starred this file. It is not present if no users have starred it. The `is_starred` property is present and true if the calling user has starred the file, else
it is omitted.

The `pinned_to` array contains the IDs of any channels to which the file is currently pinned.

The `reactions` property contains any reactions that have been added to the file and gives information about the type of reaction, the total number of users who added that reaction and a (possibly incomplete) list of users who have added that reaction to the file. The users array in the `reactions` property might not always contain all users that have reacted (we limit it to X users, and X might change), however `count` will always represent the count of all users who made that reaction (i.e. it may be greater than `users.length`).

If the authenticated user has a given reaction then they are guaranteed to appear in the `users` array, regardless of whether `count` is greater than `users.length` or not.

The `initial_comment` will be a comment from the file uploader, and will only be set when the uploader commented on the file at the time of upload. Clients can use this to display the comment with the file when announcing new file uploads. Use `comments_count` to determine how many comments are attached to a file.

## File types

Possible `filetype` values include, but are not limited to the following:

<table id="file_types">
	<tbody>
		<tr>
			<th>Type</th>
			<th>Description</th>
		</tr><tr>
			<td><code>auto</code></td><td>Auto Detect Type</td>
		</tr><tr>
			<td><code>text</code></td><td>Plain Text</td>
		</tr><tr>
			<td><code>applescript</code></td><td>AppleScript</td>
		</tr><tr>
			<td><code>boxnote</code></td><td>BoxNote</td>
		</tr><tr>
			<td><code>c</code></td><td>C</td>
		</tr><tr>
			<td><code>csharp</code></td><td>C#</td>
		</tr><tr>
			<td><code>cpp</code></td><td>C++</td>
		</tr><tr>
			<td><code>css</code></td><td>CSS</td>
		</tr><tr>
			<td><code>csv</code></td><td>CSV</td>
		</tr><tr>
			<td><code>clojure</code></td><td>Clojure</td>
		</tr><tr>
			<td><code>coffeescript</code></td><td>CoffeeScript</td>
		</tr><tr>
			<td><code>cfm</code></td><td>Cold Fusion</td>
		</tr><tr>
			<td><code>d</code></td><td>D</td>
		</tr><tr>
			<td><code>dart</code></td><td>Dart</td>
		</tr><tr>
			<td><code>diff</code></td><td>Diff</td>
		</tr><tr>
			<td><code>dockerfile</code></td><td>Docker</td>
		</tr><tr>
			<td><code>erlang</code></td><td>Erlang</td>
		</tr><tr>
			<td><code>fsharp</code></td><td>F#</td>
		</tr><tr>
			<td><code>fortran</code></td><td>Fortran</td>
		</tr><tr>
			<td><code>go</code></td><td>Go</td>
		</tr><tr>
			<td><code>groovy</code></td><td>Groovy</td>
		</tr><tr>
			<td><code>html</code></td><td>HTML</td>
		</tr><tr>
			<td><code>handlebars</code></td><td>Handlebars</td>
		</tr><tr>
			<td><code>haskell</code></td><td>Haskell</td>
		</tr><tr>
			<td><code>haxe</code></td><td>Haxe</td>
		</tr><tr>
			<td><code>java</code></td><td>Java</td>
		</tr><tr>
			<td><code>javascript</code></td><td>JavaScript/JSON</td>
		</tr><tr>
			<td><code>kotlin</code></td><td>Kotlin</td>
		</tr><tr>
			<td><code>latex</code></td><td>LaTeX/sTeX</td>
		</tr><tr>
			<td><code>lisp</code></td><td>Lisp</td>
		</tr><tr>
			<td><code>lua</code></td><td>Lua</td>
		</tr><tr>
			<td><code>markdown</code></td><td>Markdown (raw)</td>
		</tr><tr>
			<td><code>matlab</code></td><td>MATLAB</td>
		</tr><tr>
			<td><code>mumps</code></td><td>MUMPS</td>
		</tr><tr>
			<td><code>ocaml</code></td><td>OCaml</td>
		</tr><tr>
			<td><code>objc</code></td><td>Objective-C</td>
		</tr><tr>
			<td><code>php</code></td><td>PHP</td>
		</tr><tr>
			<td><code>pascal</code></td><td>Pascal</td>
		</tr><tr>
			<td><code>perl</code></td><td>Perl</td>
		</tr><tr>
			<td><code>pig</code></td><td>Pig</td>
		</tr><tr>
			<td><code>post</code></td><td>Slack Post</td>
		</tr><tr>
			<td><code>powershell</code></td><td>Powershell</td>
		</tr><tr>
			<td><code>puppet</code></td><td>Puppet</td>
		</tr><tr>
			<td><code>python</code></td><td>Python</td>
		</tr><tr>
			<td><code>r</code></td><td>R</td>
		</tr><tr>
			<td><code>ruby</code></td><td>Ruby</td>
		</tr><tr>
			<td><code>rust</code></td><td>Rust</td>
		</tr><tr>
			<td><code>sql</code></td><td>SQL</td>
		</tr><tr>
			<td><code>sass</code></td><td>Sass</td>
		</tr><tr>
			<td><code>scala</code></td><td>Scala</td>
		</tr><tr>
			<td><code>scheme</code></td><td>Scheme</td>
		</tr><tr>
			<td><code>shell</code></td><td>Shell</td>
		</tr><tr>
			<td><code>smalltalk</code></td><td>Smalltalk</td>
		</tr><tr>
			<td><code>swift</code></td><td>Swift</td>
		</tr><tr>
			<td><code>tsv</code></td><td>TSV</td>
		</tr><tr>
			<td><code>vb</code></td><td>VB.NET</td>
		</tr><tr>
			<td><code>vbscript</code></td><td>VBScript</td>
		</tr><tr>
			<td><code>velocity</code></td><td>Velocity</td>
		</tr><tr>
			<td><code>verilog</code></td><td>Verilog</td>
		</tr><tr>
			<td><code>xml</code></td><td>XML</td>
		</tr><tr>
			<td><code>yaml</code></td><td>YAML</td>
		</tr>
	</tbody>
</table>
