
This method returns a list of all users in the team. This includes deleted/deactivated users.


## Arguments

{ARGS}


## Response

Returns a list of [user objects](/types/user), in no particular order:


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


## Errors

{ERRORS}
