###Getting Message History

**Get message history for users**

To get message history for a user, one needs to call `getUserThreadHistory()` function from the `iFlyChatService` object and pass the various required parameters.

~~~ {.language-java}
service.getUserThreadHistory(fromUserId, toUserName, messageId);
~~~  
After calling this function, iFlyChat servers will send the thread history for the user. After processing the message, iFlyChatLibrary will send an intent with intent action named `iFlyChat.onUserThreadHistory`.

To listen and receive this intent, the user needs to add receiver to the application. Then user can retrieve the `userId` string using `forUserId` String and `<LinkedHashMap<String,iFlyChatMessage>` object from the intent using `threadHistoryMap` string. This `LinkedHashMap<String, iFlyChatMessage>` contains `messageId` string as String object and `iFlyChatMessage` objects from thread history.

~~~ {.language-java}
if (intent.getAction().equals("iFlyChat.onUserThreadHistory")){
    String userId = intent.getStringExtra("forUserId");

    LinkedHashMap<String, iFlyChatMessage> threadHistoryMessageMap
    = (LinkedHashMap<String, iFlyChatMessage>) intent.getSerializableExtra("threadHistoryMap");
        
        if(threadHistoryMessageMap!=null && threadHistoryMessageMap.size()>0){
            
            for (Map.Entry<String, iFlyChatMessage> entry : threadHistoryMessageMap.entrySet()) {
                iFlyChatMessage message = entry.getValue();
            }

        }
}
~~~  
NOTE: If the thread history is empty, iFlyChatLibrary will send an intent with an `userId` string, which can be retrieve using `forUserId` string and an empty `LinkedHashMap<String, iFlyChatMessage>` object, which can be retrieve using `threadHistoryMap` string.

**Get message history for rooms**

To get message history for a room, one needs to call `getRoomThreadHistory()` function from the `iFlyChatService` object and pass the various required parameters.

~~~ {.language-java}
service.getRoomThreadHistory(fromRoomId, toRoomName, messageId);
~~~  
After calling this function, iFlyChat servers will send the thread history for the room. After processing the message, iFlyChatLibrary will send an intent with intent action named `iFlyChat.onRoomThreadHistory`.

To listen and receive this intent, the user needs to add receiver to the application. Then user can retrieve the `roomId` string using `forRoomId` String and `<LinkedHashMap<String,iFlyChatMessage>` object from the intent using `threadHistoryMap` string. This `LinkedHashMap<String, iFlyChatMessage>` contains `messageId` string as String object and `iFlyChatMessage` objects from thread history.

~~~ {.language-java}
if (intent.getAction().equals("iFlyChat.onRoomThreadHistory")){
    String roomId = intent.getStringExtra("forRoomId");

    LinkedHashMap<String, iFlyChatMessage> threadHistoryMessageMap 
    = (LinkedHashMap<String, iFlyChatMessage>) intent.getSerializableExtra("threadHistoryMap");
    
        if(threadHistoryMessageMap!=null && threadHistoryMessageMap.size()>0){
    
            for (Map.Entry<String, iFlyChatMessage> entry : threadHistoryMessageMap.entrySet()) {
                iFlyChatMessage message = entry.getValue();
            }

        }
}
~~~  
NOTE: If the thread history is empty, iFlyChatLibrary will send an intent with an `roomId` string, which can be retrieve using `forRoomId` string and an empty `LinkedHashMap<String, iFlyChatMessage>` object, which can be retrieve using `threadHistoryMap` string.
