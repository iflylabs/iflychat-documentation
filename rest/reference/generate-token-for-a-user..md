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
| `user_id` | String | The id of the user |
| `user_name` | String | The name of the user |
| `user_profile_url` | String | The profile link of the user (optional) |
| `user_avatar_url` | String | The avatar URL of the user (optional) |
| `user_status` | String | The status of the user (optional) |
| `user_role` | Array | The roles array. It should contain all the roles of the user (as an associative array) (optional) |
| `user_groups` | Array | The group array. It should contain all the groups of the user (as an associative array) (optional) |
| `user-roster_list` | Array | The contact list of the user (optional) |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `Object` | JSON | It would contain the key and expires_in. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/token/generate -d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW5\", \"user_id\":\"3\", \"user_name\":"\guest123\"}"

~~~

**Response**

This is the sample response:

~~~

{"key":"TKT5GPrztRMTPMTPQWaf2Ou6LFEHVBDi1xtCkH2xBSdEV8gnZcy3eFoLp114527666063106ZeQfjRCWWVlXlWJbWuivoJvJznMDiT6ltp9ACKlPGWjhhqPHsH6xWIMn","expires_in ":"67770"}

~~~

