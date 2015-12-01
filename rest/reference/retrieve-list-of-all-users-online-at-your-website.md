###How to retrieve list of all Users Online at your website using iFlyChat API

You can use iFlyChat API to programmatically retrieve list of all users currently online at your website.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| https://api.iflychat.com/api/1.1/users/list | POST |

**Request Attribute**

This HTTP request should include following parameters:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| api_key | String | The private API key of your website |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| Object | JSON | It would contain user_id, user_name, user_role, user_status, user_avatar_url and user_profile_url of all users online at your website. It also contains the total users online at your website. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/room/create -d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW5\"}"

~~~

**Response**

This is the sample response:

{
"users": [
    {
    "user_id": "1",
    "user_role": "admin",
    "user_name": "shashwat",
    "user_status": "1",
    "user_avatar_url": "/sites/default/files/styles/thumbnail/public/pictures/picture-1-1427288050.jpg?itok=glXtBjnp",
    "user_profile_url": "javascript:void(0)"
    },
    {
    "user_id": "2",
    "user_role": "admin",
    "user_name": "shubham",
    "user_status": "1",
    "user_avatar_url": "/sites/all/modules/drupalchat/themes/light/images/default_avatar.png",
    "user_profile_url": "javascript:void(0)"
    },
  ],
  "length": 2
}
