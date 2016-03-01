
This method returns a list of all channels in the team. This includes channels the caller is in, channels they are not currently in, and archived channels but does not include private channels. The number of (non-deactivated) members in each channel is also returned.

To retrieve a list of private channels, use [`groups.list`](/methods/groups.list).


## Arguments

{ARGS}


## Response

Returns a list of limited [channel objects](/types/channel):

	{
	    "ok": true,
	    "channels": [
	        {
	            "id": "C024BE91L",
	            "name": "fun",
	            "created": 1360782804,
	            "creator": "U024BE7LH",
	            "is_archived": false,
	            "is_member": false,
	            "num_members": 6,
	            "topic": {
	                "value": "Fun times",
	                "creator": "U024BE7LV",
	                "last_set": 1369677212
	            },
	            "purpose": {
	                "value": "This channel is for fun",
	                "creator": "U024BE7LH",
	                "last_set": 1360782804
	            }
	        },
	        ....
	    ]
	}

To get a full [channel object](/types/channel), call the [channels.info](/methods/channels.info) method.


## Errors

{ERRORS}

## Warnings

{WARNINGS}
