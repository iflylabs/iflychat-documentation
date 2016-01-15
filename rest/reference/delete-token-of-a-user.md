###How to Delete Token of a User using iFlyChat API

You can use iFlyChat API to programmatically delete token of a user.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| `https://api.iflychat.com/api/1.1/token/{id}/delete` | POST |

**Request Attribute**

This HTTP request should include following parameters:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `api_key` | String | The private API key of your website |

**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `Object` | JSON | It would return { success: true }. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/token/sXt4R2YGi8POXUSKYLVtbQRsTw5BbWPyJNqaCbvwPhXVcDMVc6Oc52J8K01452852181691WfByfYhrtlaVGKAngexwIDPUIoIG6ePAJPhZSr8XACwqUrQS7xcm1IPpV/delete -d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9TutUic4Dgb-gc7RGzuZvKqZgW5\"}"

~~~

**Response**

This is the sample response:

~~~

{
  "success": true
}

~~~

