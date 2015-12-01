###How to create a new room using iFlyChat API

You can use iFlyChat API to programmatically create a new global or private room.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| https://api.iflychat.com/api/1.1/room/create | POST |

**Request Attribute**

This HTTP request should include following parameters:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| api_key | String | The private API key of your website |
| room_name | String | name of the new room to be created |
| room_role | String | The room role identifier. This determines access to room based upon user role. For example, in Drupal room role id for anonymous user is 1, and for authenticted users it is 2. |
| room_private | String | 1 if the room is going to be private (optional) |
| room_moderate | String | 1 if the room is going to be moderate (optional) |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| Object | JSON | It would contain room_id of this newly created room which you can store in your database for internal mapping. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/room/create -d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW5\", \"room_name\": \"test_room\", \"room_role\": \"1\"}"

~~~

**Response**

This is the sample response:

~~~

{
  "room_id": 5
}

~~~
