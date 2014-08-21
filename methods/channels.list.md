
This method returns a list of all channels in the team. This includes channels the caller is in, channels
they are not currently in, and archived channels. The number of (non-deactivated) members in each channel
is also returned.


## Arguments

{ARGS}


## Response

Returns a list of [channel objects](/types/channel):

	{
	    "ok": true,
	    "channels": [
	        {
	            "id": "C024BE91L",
	            "name": "fun",
	            "created": "1360782804",
	            "creator": "U024BE7LH",
	            "is_archived": false,
	            "is_member": false,
	            "num_members": 6,
	            "topic": {
	                "value": "Fun times",
	                "creator": "U024BE7LV",
	                "last_set": "1369677212"
	            },
	            "purpose": {
	                "value": "This channel is for fun",
	                "creator": "U024BE7LH",
	                "last_set": "1360782804"
	            }
	        },
	        ....
	    ]
	}


## Errors

{ERRORS}
