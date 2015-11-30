You can use iFlyChat API to programmatically create a new global or private room. To do so, make a HTTP POST request to the following URL: https://api.iflychat.com/api/1.0/room/create.

 

This HTTP request should include following parameters:

 

api_key - The private API key of your website
room_name - Name of the new room to be created
room_role - The room role identifier. This determines access to room based upon user role. For example, in Drupal room role id for anonymous users is 1, and for authenticted users it is 2.
room_private - 1 if this room is going to be private (optional)     
The response would be JSON encoded. It would contain room_id of this newly created room which you can store in your database for internal mapping.

 

Sample Code:

<?php

$ch = curl_init(); 
 
$req_url = 'https://api.iflychat.com/api/1.0/room/create'; 
 
curl_setopt($ch, CURLOPT_URL, $req_url); 
 
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
 
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, 0); 
 
curl_setopt($ch, CURLOPT_POST, true); 
 
curl_setopt($ch, CURLOPT_POSTFIELDS, 'api_key=XXXXXX&room_name=New_Room&room_role=0&room_private=1'); 
 
$result = curl_exec($ch); 
 
curl_close($ch);
 
print_r($result);
 
 
?>
 

Please note that you should be using an Enterprise plan in order to be able to use this feature.
