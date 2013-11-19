
This method returns a list of all users in the team. This includes deleted/deactivated users.


## Arguments

{ARGS}


## Response

	{
	    "ok": true,
	    "members": [
	        {
	            "id": "U023BECGF",
	            "name": "bobby",
	            "deleted": false,
	            "color": "9f69e7",
	            "profile": {
	                "first_name": "Bobby",
	                "last_name": "Tables",
	                "real_name": "Bobby Tables",
	                "email": "bobby@slack.com",
	                "skype": "my-skype-name",
	                "phone": "+1 (123) 456 7890",
	                "image_24": "https:\/\/...",
	                "image_32": "https:\/\/...",
	                "image_48": "https:\/\/...",
	                "image_72": "https:\/\/...",
	                "image_192": "https:\/\/..."
	            },
	            "is_admin": true,
	            "is_owner": true,
	            "has_files": true
	        },
	        ...
	    ]
	}

The `members` array contains 1 or more members of the team, in no particular order. For deactivated users,
`deleted` will be `true`. The `color` field is used in some clients to display a colored 
username.

The `profile` hash contains as much profile information as the user has supplied - only the `image_*`
fields are guaranteed to be included. Data that has not been supplied may not be present at all, may be `null` or 
may contain the empty string (`""`).

The `image_*` fields will always contain `https` URLs to square, web-viewable images (GIFs, JPEGs or PNGs).


## Errors

{ERRORS}
