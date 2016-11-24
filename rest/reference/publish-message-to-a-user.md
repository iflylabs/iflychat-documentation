###How to publish message to a chat room using iFlyChat API

You can use iFlyChat API to programmatically publish message to a user.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| `https://api.iflychat.com/api/1.1/user/{id}/publish` | POST |

where `{id}` is the id of the user to whom you want to send message(receiver).

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
| `roles` | Array | The roles array. It should contain all the roles of the sending user (as an associative array) |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `Object` | JSON | It would return {success: true}. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -F "api_key=Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW55" -F "uid=7" -F "name=test1" -F "picture_url=https://api.iflychat.com/sites/default/files/styles/thumbnail/public/pictures/picture-5-1427286796.jpg?itok=T_MyAL4_" -F "profile_url=javascript:void(0)" -F "message=HELLO"  -F "roles[authenticated]=authenticated" -X POST "https://api.iflychat.com/api/1.1/user/2/publish"

~~~

**Response**

This is the sample response:

~~~

{
  "success": true
}

~~~
