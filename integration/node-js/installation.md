## iFlyChat
A real time enterprise chat solution.

#### Installation
```
$ npm install iflychat
```

#### Usage
**Step 1:** Generate APP ID and API Key from iflychat.com and use these credentials in your module.
```
var iFlyChat = require('iflychat'); //load iflychat module.

let apiKey = 'your-api-key';
let appId = 'your-app-id';

iFlyChat.init(apiKey, appId);
```
**Step 2:** To create a user, you just need to call the `setUser()` function with `user_details` object as a parameter. For example,
```
var user_details = {
    'user_id': 'testUid', // string (required)
    'user_name': 'testUsername',  //string (required)
    'is_admin': false, //boolean (optional)
    'user_avatar_url': 'test-user-avatar-url', // string (optional)
    'user_profile_url': 'test-user-profile-url', // string (optional)
};

iFlyChat.setUser(user_details); 
```
**Step 4:** Now, to access iflychat you just need to call `getToken()` or `getHtmlCode()` function .

`getToken()` - it returns a `json object` on success and `false` on error.

|  property  |           values           |
|:----------:|:--------------------------:|
|     key    | 'token-to-access-iflychat' |
| expires_in |  'validity-of-chat-token'  |
```
iFlyChat.getToken(function(error, response){
    // sample response { key: 'NC1d0jeF063WZfGzzwlcrmvnXNwUs4U94mnjkUNdGlja5Jo20KxTPQmqXV1479970606204aZXKGeduLCNdpKWgUA19DrSnlEffYvCgQsj4t12HvsYkcCXbcf5r4ZH4K', expires_in: 147997059140515780 }
})
```

`getHtmlCode()` - returns `script tags to load popup chat and chat files` and `false` on error.
```
iFlyChat.getHtmlCode(function(error, response){
   //your code
})
```



