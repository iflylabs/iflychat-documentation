###Message Moderation

Users with sufficient privileges can delete messages from private and public chats.

Following is a table that details out the which operation requires admin level privileges:

| Operations                                        | Admin? |
|---------------------------------------------------|--------|
| 1. Delete other user messages from private chat   | Yes    |
| 2. Delete our own message from private chat       | No     |
| 3. Delete other user message from public chatroom | Yes    |
| 4. Delete our own message from public chatroom    | Yes    |

<br>

**Delete a message from private chat**

To delete a message from a private chat, the user needs to call a method from the iFlyChatService object and pass the message id of the message and user id from whose private chat message is to be deleted as the parameter.

```
    service.deleteChatMessageFromUser(messageId, userId);
```
<br>

If the other user has deleted the message from the private chat between you and that user, you will get a broadcast event about this. iFlyChatLibrary sends a broadcast with a message id of the message that was deleted, this broadcast intent have intent action named "iFlyChat.onMessageDeleteFromUser" so that each client can update its view right away.

To listen to this broadcast and receive the event(iFlyChat.onMessageDeleteFromUser). The user needs to match the intent action in the application's onReceive() method. To retrieve the message id string. Firstly, user needs to create and initialize the Bundle type object (bundleData). Then the user can get a messageId string by calling getString("messageId") method on data a Bundle type object :

```
if(intent.getAction().equals("iFlyChat.onMessageDeleteFromUser")){
    Bundle bundleData = intent.getExtras();
    String messageId = bundleData.getString("messageId");
}
```
<br>

**Delete a message from public chatroom**

To delete a message from public chatroom, the user needs to call a method from the iFlyChatService object and pass the message id of the message and room id from whose public chat message is to be deleted as the parameter.
```
    service.deleteChatMessageFromRoom(messageId, roomId);
```
<br>

If the other user has deleted the message from the public chatroom, every user in that chatroom will get a broadcast event about this. iFlyChatLibrary sends a broadcast with message id of the message that was deleted, this broadcast intent have intent action named "iFlyChat.onMessageDeleteFromRoom" so that each client can update its view right away.

To listen to this broadcast and receive the event(iFlyChat.onMessageDeleteFromRoom). The user needs to match the intent action in the application's onReceive() method. To retrieve the message id string. Firstly, user needs to create and initialize the Bundle type object (bundleData). Then the user can get a messageId string by calling getString("messageId") method on data a Bundle type object :

```
if(intent.getAction().equals("iFlyChat.onMessageDeleteFromRoom")){
    Bundle bundleData = intent.getExtras();
    String messageId = bundleData.getString("messageId");
}
```
<br>

###Getting Message History

**Get message history for users**

To get message history for a user, one needs to call getUserThreadHistory() function from the iFlyChatService object and pass the various required parameters.

```
    service.getUserThreadHistory(fromUserId, toUserName, messageId);
```
<br>

After calling this function, iFlyChat servers will send the thread history for the user. After processing the message, iFlyChatLibrary will send an intent with intent action named "iFlyChat.onUserThreadHistory".

To listen this intent and receive this event, the user needs to add receiver to the application and retrieve the LinkedHashMap<String, JSONArray> object from the intent using "threadHistory" string. One can get JSONArray from LinkedHashMap object using the current user userId string. This JSONArray contains iFlyChatMessage objects from thread history.

```
LinkedHashMap<String, JSONArray> threadHistoryMap = new LinkedHashMap<>();
threadHistoryMap = (LinkedHashMap<String, JSONArray>) intent.getSerializableExtra("threadHistory");
JSONArray msgObjectArray = threadHistoryMap.get(USERID);
```
<br>

NOTE: If the thread history is empty, iFlyChatLibrary will send an intent with the LinkedHashMap object, which contains an empty JSONArray.

**Get message history for rooms**

To get message history for a room, one needs to call getRoomThreadHistory() function from the iFlyChatService object and pass the various required parameters.

```
    service.getRoomThreadHistory(fromRoomId, toRoomName, messageId);
```
<br>

After calling this function, iFlyChat servers will send the thread history for the room. After processing the message, iFlyChatLibrary will send an intent with intent action named "iFlyChat.onRoomThreadHistory".

To listen this intent and receive this event, the user needs to add receiver to the application and retrieve the LinkedHashMap<String, JSONArray> object from the intent using "threadHistory" string. One can get JSONArray from LinkedHashMap object using the roomId string. This JSONArray contains iFlyChatMessage objects from that room thread history.

```
LinkedHashMap<String, JSONArray> threadHistoryMap = new LinkedHashMap<>();
threadHistoryMap = (LinkedHashMap<String, JSONArray>) intent.getSerializableExtra("threadHistory");
JSONArray msgObjectArray = threadHistoryMap.get(ROOMID);
``` 
<br>

NOTE: If the thread history is empty, iFlyChatLibrary will send an intent with the LinkedHashMap object, which contains an empty JSONArray.
<br>

###Message history moderation

Users with sufficient privileges can clear the entire message history from private and public chats.

Following is a table that details out the which operation requires admin level privileges:

| Operations                                       | Admin? |
|--------------------------------------------------|--------|
| 1. Clear message history from other private chat | No     |
| 2. Clear message history from other public chat  | Yes    |

<br>
**Clear message history from private chat**

To clear the message history from private chat, the user needs to call a function from the iFlyChatService object and pass the user id from whose private chat the message history is to be cleared, as the parameter.

```
    service.clearUserThreadHistory(userId);
```
<br>
If the other user has cleared the message history from the private chat between you and that user, you will get a broadcast event about this. iFlyChatLibrary sends a broadcast with user id of the user from whose private chat the message history was cleared. This broadcast intent have intent action named "iFlyChat.onUserThreadHistoryClear" so that each client can update its view right away.

To listen to this broadcast and receive the event(iFlyChat.onUserThreadHistoryClear). The user needs to match the intent action in the application's onReceive() method. To retrieve the user id string. Firstly, user needs to create and initialize the Bundle type object (bundleData). Then user can get userId string by calling getString("userId") method on data a Bundle type object :
```
if(intent.getAction().equals("iFlyChat.onUserThreadHistoryClear")){
    Bundle bundleData = intent.getExtras();
    String userId = bundleData.getString("userId");
}
```
<br>

**Clear the message history from public chatroom**

To clear the message history from public chatroom, the user needs to call a function from the iFlyChatService object and pass the room id from where the message history is to be cleared, as the parameter.

```
    service.clearRoomThreadHistory(roomId);
```
<br>
if the other user has cleared the message history from the public chatroom, every user in that chatroom will get a broadcast event about this. iFlyChatLibrary sends a broadcast with room id of the room from where the message history was cleared. This broadcast intent have intent action named "iFlyChat.onRoomThreadHistoryClear" so that each client can update its view right away.

To listen to this broadcast and receive the event(iFlyChat.onRoomThreadHistoryClear). The user needs to match the intent action in the application's onReceive() method. To retrieve the room id string. Firstly, user needs to create and initialize the Bundle type object (data). Then user can get roomId string by calling getString("roomId") method on data a Bundle type object :
```
if(intent.getAction().equals("iFlyChat.onRoomThreadHistoryClear")){
    Bundle data = intent.getExtras();
    String roomId = data.getString("roomId");
}
```
