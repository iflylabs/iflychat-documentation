###How to Kick a User using iFlyChat API

You can use iFlyChat API to programmatically kick any user from your website.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| `https://api.iflychat.com/api/1.1/user/{id}/kick` | POST |

where `{id}` is the id of the user whom you want to kick.

**Request Attribute**

This HTTP request should include following parameters:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `api_key` | String | The private API key of your website |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `Object` | JSON | It would return {success: true}. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/user/5/kick -d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW5\"}"

~~~

**Response**

This is the sample response:

~~~

{
  "success": true
}

~~~
