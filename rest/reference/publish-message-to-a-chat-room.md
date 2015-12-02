###How to publish message to a chat room using iFlyChat API

You can use iFlyChat API to programmatically publish message to a chat room.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| `https://api.iflychat.com/api/1.1/room/{id}/publish` | POST |

where `{id}` is the id of the chat room.

**Request Attribute**

This HTTP request should include following parameters:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `api_key` | String | The private API key of your website |
| `uid` | String | The id of the user who is sending message. |
| `name` | String | The name of the user who is sending message. |
| `picture_url` | String |The avatar URL of the user who is sending message. |
| `profile_url` | String | The profile link of the user who is sending message. |
| `message` | String | The message to be published in the chat room. |
| `color` | String | The user name will be color based on hex value specified here. |
| `roles` | Array | The roles array. It should contain all the roles of the sending user (as an associative array) |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `Object` | JSON | It would return {success: true}. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/room/5/publish -d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW55\", \"uid\": \"5\", \"name\": \"anmol\", \"picture_url\": \"//web.iflychatdev.com/websites/d7/sites/default/files/styles/thumbnail/public/pictures/picture-5-1427286796.jpg?itok=T_MyAL4_\", \"profile_url\": \"javascript:void(0)\", \"message\": \"test msg\", \"color\": \"#222222\", \"roles[0]\": \"all users\"}"

~~~

**Response**

This is the sample response:

~~~

{
  "success": true
}

~~~
