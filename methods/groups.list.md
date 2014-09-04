
This method returns a list of groups in the team that the caller is in and archived groups that the caller was in.
The list of (non-deactivated) members in each group is also returned.


## Arguments

{ARGS}


## Response

Returns a list of [group objects](/types/group):

	{
	    "ok": true,
	    "groups": [
	        {
	            "id": "G024BE91L",
	            "name": "secretplans",
	            "created": "1360782804",
	            "creator": "U024BE7LH",
	            "is_archived": false,
	            "members": [
	                "U024BE7LH"
	            ],
	            "topic": {
	                "value": "Secret plans on hold",
	                "creator": "U024BE7LV",
	                "last_set": "1369677212"
	            },
	            "purpose": {
	                "value": "Discuss secret plans that no-one else should know",
	                "creator": "U024BE7LH",
	                "last_set": "1360782804"
	            }
	        },
	        ....
	    ]
	}


## Errors

{ERRORS}
