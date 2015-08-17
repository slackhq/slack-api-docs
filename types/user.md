# User Objects

A user object contains information about a team member.

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
			"image_24": "https:\/\/…",
			"image_32": "https:\/\/…",
			"image_48": "https:\/\/…",
			"image_72": "https:\/\/…",
			"image_192": "https:\/\/…"
		},
		"is_admin": true,
		"is_owner": true,
		"is_primary_owner": true,
		"is_restricted": false,
		"is_ultra_restricted": false,
		"has_2fa": false,
		"two_factor_type": 'sms',
		"has_files": true
	},

The `name` parameter indicates the username for this user, without a leading
@ sign.

For deactivated users, `deleted` will be `true`.

The `color` field is used in some clients to display a colored  username.

The `profile` hash contains as much profile information as the user has
supplied - only the `image_*` fields are guaranteed to be included. Data that
has not been supplied may not be present at all, may be `null` or  may contain
the empty string (`""`).

The `image_*` fields will always contain `https` URLs to square, web-viewable
images (GIFs, JPEGs or PNGs).

The `has_2fa` field describes whether two-step verification is enabled for this
user. This field will always be displayed if you are looking at your own user
information. If you are looking at another user's information this field will only
be displayed if you are team admin or owner.

The `two_factor_type` field is either `app` or `sms`. It will only be present if `has_2fa` is true.