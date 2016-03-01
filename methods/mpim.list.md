
This method returns a list of all multiparty direct message channels that the user has.


## Arguments

{ARGS}


## Response

Returns a list of [group objects](/types/group):

	{
	    "ok": true,
	    "groups": [
	        {
	            "id": "G024BE91L",
	            "name": "dm-messaging-user-1",
	            "created": 1360782804,
	            "creator": "U024BE7LH",
	            "is_archived": false,
	            "is_mpim": true
                "members": [
                    "U024BE7LH",
                    "U1234567890",
                    "U2345678901",
                    "U3456789012"
                ],
	            "topic": {
                    "value": "Group messaging.",
	                "creator": "U024BE7LH",
	                "last_set": 1360782804
	            },
	            "purpose": {
	                "value": "Group messaging with: @user @user_a @user_b @user_c",
	                "creator": "U024BE7LH",
	                "last_set": 1360782804
	            }
	        },
	        ....
	    ]
	}


## Errors

{ERRORS}

## Warnings

{WARNINGS}
