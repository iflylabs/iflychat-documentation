You can use iFlyChat API to programmatically retrieve list of all rooms. To do so, make an HTTP POST request to the following URL: https://api.iflychat.com/api/1.0/rooms/list.

 

This HTTP request should include following parameters:

 

api_key - The private API key of your website  
 

The response would be JSON encoded. It would contain room_id, room_name, room_role and role_private for all rooms of your website.

Please note that you should be using an Enterprise plan in order to be able to use this feature.
