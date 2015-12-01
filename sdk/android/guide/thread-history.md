###Getting Message History

**Get message history for users**

To get message history for a user, one needs to call `getUserThreadHistory()` function from the `iFlyChatService` object and pass the various required parameters.

```
service.getUserThreadHistory(fromUserId, toUserName, messageId);
```
<br>

After calling this function, iFlyChat servers will send the thread history for the user. After processing the message, iFlyChatLibrary will send an intent with intent action named `iFlyChat.onUserThreadHistory`.

To listen this intent and receive this event, the user needs to add receiver to the application and retrieve the `LinkedHashMap<String, JSONArray>` object from the intent using `threadHistory` string. One can get `JSONArray` from `LinkedHashMap` object using the current user userId string. This `JSONArray` contains `iFlyChatMessage` objects from thread history.

```
LinkedHashMap<String, JSONArray> threadHistoryMap = new LinkedHashMap<>();
threadHistoryMap = (LinkedHashMap<String, JSONArray>) intent.getSerializableExtra("threadHistory");
JSONArray msgObjectArray = threadHistoryMap.get(USERID);
```
<br>

NOTE: If the thread history is empty, iFlyChatLibrary will send an intent with the `LinkedHashMap` object, which contains an empty `JSONArray`.

**Get message history for rooms**

To get message history for a room, one needs to call `getRoomThreadHistory()` function from the `iFlyChatService` object and pass the various required parameters.

```
service.getRoomThreadHistory(fromRoomId, toRoomName, messageId);
```
<br>

After calling this function, iFlyChat servers will send the thread history for the room. After processing the message, iFlyChatLibrary will send an intent with intent action named `iFlyChat.onRoomThreadHistory`.

To listen this intent and receive this event, the user needs to add receiver to the application and retrieve the `LinkedHashMap<String, JSONArray>` object from the intent using `threadHistory` string. One can get `JSONArray` from `LinkedHashMap` object using the roomId string. This `JSONArray` contains `iFlyChatMessage` objects from that room thread history.

```
LinkedHashMap<String, JSONArray> threadHistoryMap = new LinkedHashMap<>();
threadHistoryMap = (LinkedHashMap<String, JSONArray>) intent.getSerializableExtra("threadHistory");
JSONArray msgObjectArray = threadHistoryMap.get(ROOMID);
``` 
<br>

NOTE: If the thread history is empty, iFlyChatLibrary will send an intent with the `LinkedHashMap` object, which contains an empty `JSONArray`.
