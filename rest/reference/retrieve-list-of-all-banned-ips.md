###How to retrieve list of all Banned Ips using iFlyChat API

You can use iFlyChat API to programmatically retrieve list of all ips banned from your website.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| https://api.iflychat.com/api/1.1/ips/banned/list | POST |

**Request Attribute**

This HTTP request should include following parameters:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| api_key | String | The private API key of your website |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| Object | JSON | It would contain ip of all users banned at your website.. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/ips/banned/list -d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW5\"}"

~~~

**Response**

This is the sample response:

~~~

[
  {
    "ip": "182.71.119.146"
  }
]

~~~
