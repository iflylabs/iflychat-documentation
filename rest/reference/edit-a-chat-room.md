<h3>How to edit a room using iFlyChat API</h3>

<p>You can use iFlyChat API to programmatically edit any room.</p>

<p><strong>Header Table</strong></p>

<p>Make a&nbsp;HTTP POST request to the following url:</p>

<table border="1" cellpadding="1" cellspacing="1" style="line-height:20.7999992370605px; width:500px">
	<tbody>
		<tr>
			<td><strong>Url</strong></td>
			<td><strong>Type</strong></td>
		</tr>
		<tr>
			<td>
			<p>https://{networkName}.iflychat.com/api/1.1/room/{id}/edit</p>
			</td>
			<td>POST</td>
		</tr>
	</tbody>
</table>

<p>where {id} is the id room which you want to edit.</p>

<p><strong>Request Attribute</strong></p>

<p>This HTTP request should include following parameters:</p>

<table border="1" cellpadding="1" cellspacing="1" style="line-height:20.7999992370605px; width:500px">
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
			<td>The room role identifier. This determines access to room based upon user role. For example, in Drupal room role id for anonymous user is 1, and for authenticted users it is 2.</td>
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

<table border="1" cellpadding="1" cellspacing="1" style="line-height:20.7999992370605px; width:500px">
	<tbody>
		<tr>
			<td><strong>Attribute</strong></td>
			<td><strong>Type</strong></td>
			<td><strong>Description</strong></td>
		</tr>
		<tr>
			<td>Object&nbsp;</td>
			<td>JSON</td>
			<td>It would return object {"success": true}</td>
		</tr>
	</tbody>
</table>

<p><strong>Curl Command</strong></p>

<p>This the sample&nbsp;curl command required to make HTTP request:</p>

<pre>
curl -H "Content-Type: application/json" -X POST&nbsp;https://api.iflychat.com/api/1.1/room/4/edit&nbsp;-d "{\"api_key\":\"Wr4vpoJ_ET3lpBdX9E9TukjzDF62L-gc7RGzuZvKqZgW5\", \"room_name\": \"room_4\", \"room_role\": \"1\", \"room_private\": \"1\", \"room_moderate\": \"1\"}"</pre>

<p><strong>Response</strong></p>

<p>This is the sample response:</p>

<pre>
{
  "success": true
}</pre>
