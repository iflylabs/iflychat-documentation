<h3>How to create a new room using iFlyChat API</h3>

<p>You can use iFlyChat API to programmatically create a new global or private room.</p>

<p><strong>Header Table</strong></p>

<p>Make a&nbsp;HTTP POST request to the following url:</p>

<table border="1" cellpadding="1" cellspacing="1" style="width:400px">
	<tbody>
		<tr>
			<td><strong>Url</strong></td>
			<td><strong>Type</strong></td>
		</tr>
		<tr>
			<td>
			<p>https://{networkName}.iflychat.com/api/1.1/room/create</p>
			</td>
			<td>POST</td>
		</tr>
	</tbody>
</table>

<p><strong>Request Attribute</strong></p>

<p>This HTTP request should include following parameters:</p>

<table border="1" cellpadding="1" cellspacing="1" style="width:500px">
	<tbody>
		<tr>
			<td><strong>Attribute</strong></td>
			<td><strong>Type</strong></td>
			<td><strong>Description</strong></td>
		</tr>
		<tr>
			<td>api_key</td>
			<td>String</td>
			<td>The private API key of your website.</td>
		</tr>
		<tr>
			<td>room_name</td>
			<td>String</td>
			<td>Name of the new room to be created.</td>
		</tr>
		<tr>
			<td>room_role</td>
			<td>String</td>
			<td>
			<p>The room role identifier. This determines access to room based upon user role. For example, in Drupal room role id for anonymous user is 1, and for authenticted users it is 2.</p>
			</td>
		</tr>
		<tr>
			<td>room_private</td>
			<td>String</td>
			<td>1 if the room is going to be private (optional)</td>
		</tr>
		<tr>
			<td>room_moderate</td>
			<td>String</td>
			<td>1 if the room is going to be moderate (optional)</td>
		</tr>
	</tbody>
</table>

<p><strong>Response Attribute</strong></p>

<p>The response would be following:</p>

<table border="1" cellpadding="1" cellspacing="1" style="width:500px">
	<tbody>
		<tr>
			<td>Attribute&nbsp;</td>
			<td>Type</td>
			<td>Description</td>
		</tr>
		<tr>
			<td>Object</td>
			<td>JSON</td>
			<td>It would contain room_id of this newly created room which you can store in your database for internal mapping.</td>
		</tr>
	</tbody>
</table>

<p><strong>Curl Command</strong></p>

<p>This the sample&nbsp;curl command required to make HTTP request:</p>

<pre>
curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/room/create -d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9Tuk
jzDF62L-gc7RGzuZvKqZgW5\", \"room_name\": \"test_room\", \"room_role\": \"1\"}"</pre>

<p><strong>Response</strong></p>

<p>This is the sample response:</p>

<pre>
{
  "room_id": 5
}</pre>
