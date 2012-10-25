# Error Codes

* 1 Missing or invalid format - request not ending with .json or .xml
* 2 Request was not signed with OAuth Token
* 4 Request was signed, but the signature was invalid
* 8 Request was signed, but the user is unknown
* 16 No action was specified
* 32 A method that requires POST was requested using GET
* 128 Missing required parameter
* 136 Parameter must be an integer and a non integer value was passed
* 144 Integer value passed is too small
* 152 Integer value passed is too big
* 160 Parameter must be an float and a non float value was passed
* 192 String parameter is too short
* 200 String parameter is too long
* 1000 User has no credits
* 1500 Generic Server Error
* 2000 Camera not found
* 2001 Not owner of the camera
* 2002 Live View not available for the camera
* 2003 Live View is not connected
* 3000 Item not found
* 3001 User does not have permission to view this item
* 3002 User is not the owner of the item, required for delete, update, move, copy
* 3003 Item is already in the folder when attempting move, copy
* 3004 Folder does not belong to user when attempting move, copy, save_snapshot
* 3005 Folder does not exist when attempting move, copy, save_snapshot
* 3006 Item is already a snapshot when attempting save_snapshot
* 3007 Identifier is not part of the clip when attempting save_snapshot
* 3008 Cannot restore item - too long in trash
* 3009 Invalid datetime passed to get_list
* 4000 Folder not found
* 4001 User does not have permission to view this folder's subfolders
* 4002 User is not the owner of the folder
* 4003 Folder is already a child of the parent folder when attempting move
* 4004 Name already exists when attempting folder rename
* 4005 Name already exists when attempting folder create
* 4100 Parent folder does not exist
* 4102 User is not owner of parent folder
* 5000 Network not found
* 5001 User does not have permission to view the network details (i.e. network is hidden and user is not a member)
* 5002 User is not a member of the network
* 5003 User is not the owner of the network
* 5004 Invalid type passed to update
* 5005 No fields passed when attempting update
* 5100 Invitation does not exist
* 5101 Unknown username
* 5102 User not member of the network
* 5200 Thread not found
* 5300 Passed both thread_id and network_id when attempting forum_postmessage
* 5400 Network not public when attempting to join
* 5401 The network requires cameras to join
* 5402 User already is a member of network when attempting to join
* 5410 Empty cameras list in call to join network
* 5411 Invalid camera id in cameras list passed to join network
* 5412 Non-existent camera id in cameras list passed to join network
* 5413 Camera in cameras list does not belong to user when attempting to join network
* 6000 Private message thread not found
* 6001 User does not have permission to view the thread
* 6101 User does not have permission to reply to the thread
* 6200 Cannot send private message to self
* 6201 Recipient of private message does not exist


******************

[Back to main page](../README.md)
