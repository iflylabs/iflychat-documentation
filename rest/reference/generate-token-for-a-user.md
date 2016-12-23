###How to Generate Token For a User using iFlyChat API

You can use iFlyChat API to programmatically generate token for a user.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| `https://api.iflychat.com/api/1.1/token/generate` | POST |

**Request Attribute**

This HTTP request should include following parameters:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `api_key` | String | The private API key of your website |
| `app_id` | String | The public APP ID of your website |
| `user_id` | String (< 255 characters) | The id of the user |
| `user_name` | String (< 255 characters) | The name of the user |
| `chat_role` | String | The chat role of the user. Possible values - {'admin', 'moderator, 'participant', 'viewer'} (optional) |
| `user_profile_url` | String | The profile link of the user (optional) |
| `user_avatar_url` | String | The avatar URL of the user (optional) |
| `user_status` | String | The status of the user (optional) |
| `user_list_filter` | String | The filtering parameter for showing online users (default = "all") (optional) |
| `user_roles` | Object | The roles array. It should contain all the roles of the user (as an associative array) (optional) |
| `user_site_roles` | Object | The user site roles array. It should contain all the roles of your website (as an associative array) (optional) |
| `user_groups` | Object | The group array. It should contain all the groups of the user (as an associative array) (optional) |
| `user_relationships` | Object | The contact list of the user (optional) |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `Object` | JSON | It would contain the key and expires_in. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -H "Content-Type: application/json" -X POST -d '{"api_key":"Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW5","app_id":"41357620-760b-4495-ba78-6ebddbd14f06","user_name":"ee1231efdghje1","user_id":"1","user_name":"test_user"}' https://api.iflychat.com/api/1.1/token/generate

~~~

**Response**

This is the sample response:

~~~

{"key":"TKT5GPrztRMTPMTPQWaf2Ou6LFEHVBDi1xtCkH2xBSdEV8gnZcy3eFoLp114527666063106ZeQfjRCWWVlXlWJbWuivoJvJznMDiT6ltp9ACKlPGWjhhqPHsH6xWIMn","expires_in ":"67770"}

~~~

