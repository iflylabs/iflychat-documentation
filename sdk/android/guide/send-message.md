###Sending and receiving messages

**To send a message to the user**

The first person needs to create an object of iFlyChatMessage object with the required parameters and pass that object to the iFlyChatService object's method "sendMessagetoUser(messageObject)":
```
iFlyChatMessage msgObj = new iFlyChatMessage("", currentUser.getId(), currentUser.toId() , currentUser.getName(),currentUser.toName(), messageToUser_String , "", currentUser.getProfileUrl(),currentUser.getAvatarUrl(), currentUser.getRole(), "", "user");

service.sendMessageToUser(msgObj);
```
<br>

Message text, fromName, toName, fromId, toId and type are the required parameters to create this message object otherwise the class will throw an exception.

The user should leave the message_id and time fields as empty strings because the iFlyChatLibrary itself creates those parameters and insert them into the final message that is sent to the server.

color, fromProfileUrl, fromAvatarUrl and fromRole are some of the optional parameters and can be left empty if not available.

<br>

**To send a message to the room**

The first person needs to create an object of an iFlyChatMessage object with the required parameters and pass that object to the iFlyChatService object's method "sendMessagetoRoom(messageObject)":
```
iFlyChatMessage msgObj = new iFlyChatMessage("", currentUser.getId(), currentUser.toId(), currentUser.getName(),currentUser.toName() , messageToRoom_String, "", currentUser.getProfileUrl(),currentUser.getAvatarUrl(), currentUser.getRole(), "", "room");

service.sendMessageToRoom(msgObj);
```
<br>

Message text, fromName, toName, fromId, toId and type are the required parameters to create this message object otherwise the class will throw an exception.

The user should leave the message_id and time fields as empty strings because the iFlyChatLibrary itself creates those parameters and insert them into the final message that is sent to the server.

color, fromProfileUrl, fromAvatarUrl and fromRole are some of the optional parameters and can be left empty if not available.

<br>

**Receiving message from user**

When some other user sends a message to the first user, iFlyChatLibrary sends a broadcast with the iFlyChatMessage object and this broadcast intent have intent action named "iFlyChat.onMessagefromUser". Therefore, it is required that the application must listen to this broadcast in order to receive the message from the user and then the user can process the message.

To listen to this broadcast and receive the event(iFlyChat.onMessageFromUser), the user needs to match the intent action in the application's onReceive() method and retrieve the iFlyChatMessage object from the broadcast:
```
if (intent.getAction().equals("iFlyChat.onMessageFromUser")) {
    iFlyChatMessage messageObject = intent.getParcelableExtra("messsageObj");
}
```
<br>

There are several getter methods which gives you some properties of the iFlyChatMessage object. Which you can use to show in the UI. These getter methods are explained in the javadoc of the iFlyChatLibrary.

**Example:**
```
Toast.makeText(context,"onMessageFromUser: " + messageObject.getMessageId() + " " + messageObject.getFromId() + " " + messageObject.getToId() 
    + " " + messageObject.getFromName() + " " + messageObject.getToName() + " " + messageObject.getMessage() + " " + messageObject.getFromColor()+ " " + messageObject.getFromProfileUrl() + " " + messageObject.getFromAvatarUrl() + " " + messageObject.getFromRole() 
    + " " + messageObject.getTime() + " " + messageObject.getType(), Toast.LENGTH_LONG).show();
```
<br>

**Receiving message from room**

When some other user sends a message to a room, iFlyChatLibrary sends a broadcast with the iFlyChatMessage object and this broadcast intent have intent action named "iFlyChat.onMessagefromRoom". Therefore, it is required that the application must listen to this broadcast in order to receive the message from the room and then the user can process the message.

To listen to this broadcast and receive the event(iFlyChat.onMessageFromRoom), the user needs to match the intent action in the application's onReceive() method and retrieve the iFlyChatMessage object from the broadcast:
```
if (intent.getAction().equals("iFlyChat.onMessageFromRoom")) {
    iFlyChatMessage messageObject = intent.getParcelableExtra("messsageObj");
}
```
<br>
