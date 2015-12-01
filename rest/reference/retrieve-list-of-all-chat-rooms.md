###How to retrieve list of all chat rooms using iFlyChat API

You can use iFlyChat API to programmatically retrieve list of all chat rooms.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| https://api.iflychat.com/api/1.1/rooms/list | POST |

**Request Attribute**

This HTTP request should include following parameters:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| api_key | String | The private API key of your website |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| Object | JSON | It would contain room_id, room_name, room_role and role_private for all rooms of your website. It also contains length of the total rooms. |

**Curl Command**

This the sample curl command required to make HTTP request:

` curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/rooms/list -d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW5\"}" `

**Response**

This is the sample response:

{
  "room_id": 5
}
