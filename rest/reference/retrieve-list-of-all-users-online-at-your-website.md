You can use iFlyChat API to programmatically retrieve list of all users currently online at your website. To do so, make an HTTP POST request to the following URL: https://api.iflychat.com/api/1.0/users/list.

 

This HTTP request should include following parameters:

 

api_key - The private API key of your website  
 

The response would be JSON encoded. It would contain id, name, status and pic for all users online at of your website.

Please note that you should be using an Enterprise plan in order to be able to use this feature.
