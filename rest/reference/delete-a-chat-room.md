You can use iFlyChat API to programmatically delete any chat room. To do so, make a HTTP POST request to the following URL: https://api.iflychat.com/api/1.0/room/{id}/delete, where {id} is the id of the room which you want to delete.

 

This HTTP request should include following parameters:

 

api_key - The private API key of your website   
 

The response would be JSON encoded.

Please note that you should be using an Enterprise plan in order to be able to use this feature.
