You can use iFlyChat API to programmatically kick any user from your website. To do so, make a HTTP POST request to the following URL: https://api.iflychat.com/api/1.0/user/{id}/kick, where {id} is the id of the user whom you want to kick.

 

This HTTP request should include following parameters:

 

api_key - The private API key of your website   
 

The response would be JSON encoded. It would contain 1 if successful.

Please note that you should be using an Enterprise plan in order to be able to use this feature.
