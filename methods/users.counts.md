
This method returns a list of all channels, groups and direct message channels open to the user. This
*does not* include public channels that the calling user is not a member of, but it does include
direct message channels which are currently not 'open' (but in which the caller is a participant).

Each channel/group/DM contains a count of unread messages, mentions and DMs. This can be used to quickly
show a summary of unread messages without fetching history for all channels.


## Arguments

{ARGS}


## Response

	{
	    "ok": true,
	    "channels": [
	        {
	            "id": "C024BFDJ1",
	            "name": "bieber_tweets",
	            "unread_count": 0,
	            "unread_count_display": 0,
	            "mention_count": 0
	        },
	        ...
	    ],
	    "groups": [
	        {
	            "id": "G024G5PN0",
	            "name": "secrets",
	            "unread_count": 0,
	            "unread_count_display": 0,
	            "mention_count": 0
	        },
	        ...
	    ],
	    "ims": [
        	{
	            "id": "D024BFE7G",
	            "name": "slackbot",
	            "dm_count": 0
	        },
	        {
	            "id": "D024BEBJP",
	            "name": "ali",
	            "dm_count": 0
	        },
	        ...
	    ]
	}


## Errors

{ERRORS}
