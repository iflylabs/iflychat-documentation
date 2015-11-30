You can use iFlyChat REST API to programmatically publish message to a chat room. To do so, make a HTTP POST request to the following URL: https://api.iflychat.com/api/1.0/room/{id}/publish, where {id} is the id of the chat room.

 

This HTTP request should include following parameters:

 

api_key - The private API key of your website 
uid - The id of the user who is sending message 
name - The name of the user who is sending message 
picture_url - The avatar URL of the user who is sending message 
profile_url - The profile link of the user who is sending messagerivate API key of your website 
message - The message to be published in the chat room 
color - The user name will be colored based on HEX value specified here. Example - #222222 
roles - The roles array. It should contain all the roles of the sending user (as an associative array) 
 

The response would be JSON encoded.

Please note that you should be using an Enterprise plan in order to be able to use this feature.
