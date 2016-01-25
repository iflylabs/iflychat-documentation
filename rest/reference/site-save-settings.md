###How to Save site settings using iFlyChat API

You can use iFlyChat API to programmatically to save settings of site.

**Header Table**

Make a HTTP POST request to the following url:

| Url        | Type           |
| :------------- |:------------- |
| `https://api.iflychat.com/api/1.1/site-save/settings` | POST |

**Request Attribute**

This HTTP request should include following parameters:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `api_key` | String | The private API key of your website |
| `enable_default_chatroom` | Boolean | Enable public chatroom |
| `theme` | String | Theme color |
| `sound_notification` | String | To play notification sound when a new message is received |
| `smileys` | String | Show smileys |
| `chat_logging` | String | Enable log chat messages, which can be later viewed in message inbox |
| `chat_header_background_color` | String | Color of the top bar in the chat |
| `chat_header_text_color` | String | Color of the text in top bar in the chat |
| `font_color` | String | Color of the text in the chat. |
| `chat_header_text` | String | This is the text that will appear in header of chat list |
| `default_room_header_text` | String | This is the text that will appear in header of public chatroom |
| `enable_user_roster_list` | String | This determines the method for creating the chat buddylist |
| `platform_version` | String | Version of Platform |
| `clear_thread_history` | String | To apply above defined block hyperlinks setting only to anonymous users |
| `delete_messages` | String | To allow users to clear all messages in a room |
| `set_user_font_color_in_room` | Boolean | To allow users to set color of their name in a room |
| `guest_prefix` | String | Guest prefix |
| `enable_guest_change_name` | String | Allow anonymous user to be able to change his/her name|
| `use_stop_word_list` | String | To use stop words for filtering |
| `stop_word_list` | String | Stop word list |
| `file_attachment` | String | To allow user to share/upload file in chat |
| `mobile_browser_app` | String | To enable browser based mobile app |
| `mobile_sdk_integration` | String | To enable native mobile sdk integration |
| `enable_groups` | String | This determines the method for creating the chat buddylist |
| `valid_uids` | Array | The singular form of User Relationships Role Names (e.g. buddy, friend, coworker, spouse) separated by comma(optional) |
| `allRoles` | Array | The mapping of all the roles exist on the site |


**Response Attribute**

The response would be following:

| Attribute        | Type          | Description |
| :------------- |:------------- | :-------------|
| `Object` | JSON | It would contain success key with the value true. |

**Curl Command**

This the sample curl command required to make HTTP request:

~~~

curl -H "Content-Type: application/json" -X POST https://api.iflychat.com/api/1.1/token/generate -d "{\"api_key\":\"kaGTLz79GqtbcqBsY5Lcoc-AlbyCsdfghjFDFDwewe8s0W24\",\"enable_default_chatroom\":\"1\",\"theme\":\"light\",\"sound_notification\":\"1\",\"smileys\":\"1\",\"chat_logging\":\"1\",\"chat_header_background_color\":\"#222222\",\"chat_header_text_color\":\"#FFFFFF\",\"font_color\":\"#222222\",\"chat_header_text\":\"Chat\",\"default_room_header_text\":\"Public Chatroom\",\"enable_user_roster_list\":\"0\",\"platform_version\":\"7.x-1.3\",\"clear_thread_history\":\"1\",\"delete_messages\":\"1\",\"set_user_font_color_in_room\":\"1\",\"guest_prefix\":\"Guest \",\"enable_guest_change_name\":\"1\",\"use_stop_word_list\":\"1\",\"stop_word_list\":\"beastial,beastiality,smut,spunk\",\"file_attachment\":\"1\",\"mobile_browser_app\":\"1\",\"mobile_sdk_integration\":\"2\",\"enable_group\":\"2\",\"allRoles[0]\": \"anonymous user\",\"allRoles[1]\": \"authenticated user\",\"allRoles[2]\": \"administrator\"}"

~~~

**Response**

This is the sample response:

~~~

{"success":"true"}

~~~

