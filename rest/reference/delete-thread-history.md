###How to delete thread history using iFlyChat API

You can use iFlyChat API to programmatically delete thread history.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| `https://api.iflychat.com/api/1.1/threads/delete` | POST |

There are 2 different ways of deleting thread history:

1. Deleting thread history of a room

    **Request Attribute**

    This HTTP request should include following parameters:

    | Attribute        | Type          | Description |
    | :------------- |:------------- | :-------------|
    |`api_key` | String | The private API key of your website |
    | `room_id` | String | The string will contain the id of the room whose thread history you want to delete. |

    **Response Attribute**

    The response would be following:

    | Attribute        | Type          | Description |
    | :------------- |:------------- | :-------------|
    | `Object` | JSON | It would return { success: true } |

    **Curl Command**

    This the sample curl command required to make HTTP request:

    ~~~

    curl -F "api_key=Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW55" -F "room_id=10" -X POST "https://api.iflychat.com/api/1.1/threads/delete"

    ~~~

    **Response**

    This is the sample response:

    ~~~

     {
      "success": true
     },

    ~~~

2. Deleting thread history between two users

    **Request Attribute**

    This HTTP request should include following parameters:

    | Attribute        | Type          | Description |
    | :------------- |:------------- | :-------------|
    | `api_key` | String | The private API key of your website |
    | `from_id` | String | The id of the first user. |
    | `to_id` | String |The id of the second user. |

    **Response Attribute**

    The response would be following:

    | Attribute        | Type          | Description |
    | :------------- |:------------- | :-------------|
    | `Object` | JSON | It would return { success: true } |

    **Curl Command**

    This the sample curl command required to make HTTP request:

    ~~~

    curl -F "api_key=Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW55" -F "from_id=12" -F "to_id=39" -X POST "https://api.iflychat.com/api/1.1/threads/delete"

    ~~~

    **Response**

    This is the sample response:

    ~~~

    {
     "success": true
    },

    ~~~
