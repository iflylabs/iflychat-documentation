###How to retrieve thread history using iFlyChat API

You can use iFlyChat API to programmatically retrieve thread history.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| https://api.iflychat.com/api/1.1/threads/get | POST |

There are 3 different ways of retrieving thread history:

 1. Retrieving thread history of a room or list of rooms 

**Request Attribute**

This HTTP request should include following parameters:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| api_key | String | The private API key of your website |
| room_id | String/Array | This can be a string or an array. The string will contain the id of the room whose thread history you want to retrieve and the array will contain the id of the rooms whose thread history you want to retrieve. |
| start_timestamp | String | The start timestamp (in milliseconds) of the range between which you want the thread history (optional) |
| end_timestamp | String | The end timestamp (in milliseconds) of the range between which you want the thread history (optional) |
| limit | String | The number of results to be returned (optional) |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| Object | JSON | It would return thread history of that room or list of rooms with time, from_id, room_id, from_name, room_name, message, message_id as properties. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/threads/get -d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW5\", \"room_id\": \"5\", \"start_timestamp\": \"1433142614\", \"end_timestamp\": \"1433154346\", \"limit\": \"3\"}"

~~~

**Response**

This is the sample response:

~~~

[
  {
    "time": 1439793830,
    "from_id": "14",
    "room_id": "5",
    "from_name": "prateek",
    "room_name": "Mobile Room",
    "message": "hello",
    "message_id": "m_14_c-5_1439793800313"
  },
  {
    "time": 1440491549,
    "from_id": "0-14358329043yvbs",
    "room_id": "5",
    "from_name": "Guest Michael",
    "room_name": "General Room",
    "message": "how are you?",
    "message_id": "m_0-14358329043yvbs_c-5_1440491559161"
  },
  {
    "time": 1440491833,
    "from_id": "0-14358329043yvbs",
    "room_id": "5",
    "from_name": "Guest Michael",
    "room_name": "General Room",
    "message": "whats up?",
    "message_id": "m_0-14358329043yvbs_c-5_1440491842827"
  },
]

~~~
