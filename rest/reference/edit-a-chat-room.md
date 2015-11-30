You can use iFlyChat API to programmatically edit any room. To do so, make a HTTP POST request to the following URL: https://api.iflychat.com/api/1.0/room/{id}/edit, where {id} is the id of the room which you want to edit.

 

This HTTP request should include following parameters:

 

api_key - The private API key of your website
room_name - Name of the new room to be created
room_role - The room role identifier. This determines access to room based upon user role. For example, in Drupal room role id for anonymous users is 1, and for authenticted users it is 2.
room_private - 1 if this room is going to be private (optional)     
The response would be JSON encoded. It would contain room_id of this room which you can store in your database for internal mapping.

Please note that you should be using an Enterprise plan in order to be able to use this feature.
