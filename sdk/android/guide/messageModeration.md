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

<code>
service.deleteChatMessageFromUser(messageId, userId);
</code>
<br>

If the other user has deleted the message from the private chat between you and that user, you will get a broadcast event about this. iFlyChatLibrary sends a broadcast with a message id of the message that was deleted, this broadcast intent have intent action named "iFlyChat.onMessageDeleteFromUser" so that each client can update its view right away.

To listen to this broadcast and receive the event(iFlyChat.onMessageDeleteFromUser). The user needs to match the intent action in the application's onReceive() method. To retrieve the message id string. Firstly, user needs to create and initialize the Bundle type object (bundleData). Then the user can get a messageId string by calling getString("messageId") method on data a Bundle type object :

<code>
if(intent.getAction().equals("iFlyChat.onMessageDeleteFromUser")){
    Bundle bundleData = intent.getExtras();
    String messageId = bundleData.getString("messageId");
}
</code>
<br>

**Delete a message from public chatroom**

To delete a message from public chatroom, the user needs to call a method from the iFlyChatService object and pass the message id of the message and room id from whose public chat message is to be deleted as the parameter.
<code>
service.deleteChatMessageFromRoom(messageId, roomId);
</code>
<br>

If the other user has deleted the message from the public chatroom, every user in that chatroom will get a broadcast event about this. iFlyChatLibrary sends a broadcast with message id of the message that was deleted, this broadcast intent have intent action named "iFlyChat.onMessageDeleteFromRoom" so that each client can update its view right away.

To listen to this broadcast and receive the event(iFlyChat.onMessageDeleteFromRoom). The user needs to match the intent action in the application's onReceive() method. To retrieve the message id string. Firstly, user needs to create and initialize the Bundle type object (bundleData). Then the user can get a messageId string by calling getString("messageId") method on data a Bundle type object :

<code>
if(intent.getAction().equals("iFlyChat.onMessageDeleteFromRoom")){
    Bundle bundleData = intent.getExtras();
    String messageId = bundleData.getString("messageId");
}
</code>
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

<code>
service.clearUserThreadHistory(userId);
</code>
<br>
If the other user has cleared the message history from the private chat between you and that user, you will get a broadcast event about this. iFlyChatLibrary sends a broadcast with user id of the user from whose private chat the message history was cleared. This broadcast intent have intent action named "iFlyChat.onUserThreadHistoryClear" so that each client can update its view right away.

To listen to this broadcast and receive the event(iFlyChat.onUserThreadHistoryClear). The user needs to match the intent action in the application's onReceive() method. To retrieve the user id string. Firstly, user needs to create and initialize the Bundle type object (bundleData). Then user can get userId string by calling getString("userId") method on data a Bundle type object :
<code>
if(intent.getAction().equals("iFlyChat.onUserThreadHistoryClear")){
    Bundle bundleData = intent.getExtras();
    String userId = bundleData.getString("userId");
}
</code>
<br>

**Clear the message history from public chatroom**

To clear the message history from public chatroom, the user needs to call a function from the iFlyChatService object and pass the room id from where the message history is to be cleared, as the parameter.

<code>
service.clearRoomThreadHistory(roomId);
</code>
<br>
if the other user has cleared the message history from the public chatroom, every user in that chatroom will get a broadcast event about this. iFlyChatLibrary sends a broadcast with room id of the room from where the message history was cleared. This broadcast intent have intent action named "iFlyChat.onRoomThreadHistoryClear" so that each client can update its view right away.

To listen to this broadcast and receive the event(iFlyChat.onRoomThreadHistoryClear). The user needs to match the intent action in the application's onReceive() method. To retrieve the room id string. Firstly, user needs to create and initialize the Bundle type object (data). Then user can get roomId string by calling getString("roomId") method on data a Bundle type object :
<code>
if(intent.getAction().equals("iFlyChat.onRoomThreadHistoryClear")){
    Bundle data = intent.getExtras();
    String roomId = data.getString("roomId");
}
</code>
