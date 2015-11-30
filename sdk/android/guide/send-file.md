### Sending Files
**Send file to user**

To send a file to an user, take Uri of the file to be sent in string format. Set this Uri string as a message String in your `iFlyChatMessage` object `msgObj`. Then, call `sendFileToUser(iFlyChatMessage msgObj)` method of `iFlyChatService` class object.

```
service.sendFileToUser(msgObj)
```
<br>

Then, iFlyChatLibrary broadcast an intent having intent action named `iFlyChat.onUploadProgress`. In order to get and show this upload progress in your app, you need to receive this broadcast.

To listen to this broadcast and receive the event `iFlyChat.onUploadProgress`, the user needs to match the intent action in the application's `onReceive()` method and retrieve the `HashMap<String, String>` object from the broadcast:

```
if(intent.getAction().equals("iFlyChat.onUploadProgress")){
     HashMap<String, String> uploadProgressMap = (HashMap<String, String> ) intent.getSerializableExtra("onUploadProgress");
     String uploadMessageId = uploadProgressMap.get("messageId");
     String progress = uploadProgressMap.get("progress");
}
```
<br>

When the complete file upload takes place, iFlyChatLibrary sends a broadcast with the `iFlyChatMessage` object and this broadcast intent have intent action named `iFlyChat.onMessagefromUser`. This is similar to when a message come from an user. But this `iFlyChatMessage` object contains a specific url string as a message string of the file that is sent to iFlyChatLibrary. Now you can download/view the file content from this url as you want in your app. To get this `iFlyChatMessage` object receive the intent with intent action named `iFlyChat.onMessagefromUser`.

```
if (intent.getAction().equals("iFlyChat.onMessageFromUser")) {
    iFlyChatMessage messageObject = intent.getParcelableExtra("messsageObj");
}
```
<br>

**Send file to room**

To send a file to a room, take Uri of the file to be sent in string format. Set this Uri string as a message String in your `iFlyChatMessage` object `msgObj`. Then, call `sendFileToRoom(iFlyChatMessage msgObj)` method of `iFlyChatService` class object.

```
service.sendFileToRoom(msgObj)
```
<br>

Then, iFlyChatLibrary broadcast an intent having intent action named `iFlyChat.onUploadProgress`. In order to get and show this upload progress in your app, you need to receive this broadcast.

To listen to this broadcast and receive the event `iFlyChat.onUploadProgress`, the user needs to match the intent action in the application's `onReceive()` method and retrieve the `HashMap<String, String>` object from the broadcast:

```
if(intent.getAction().equals("iFlyChat.onUploadProgress")){
     HashMap<String, String> uploadProgressMap = (HashMap<String, String> ) intent.getSerializableExtra("onUploadProgress");
     String uploadMessageId = uploadProgressMap.get("messageId");
     String progress = uploadProgressMap.get("progress");
}
```
<br>

When the complete file upload takes place, iFlyChatLibrary sends a broadcast with the `iFlyChatMessage` object and this broadcast intent have intent action named `iFlyChat.onMessagefromRoom`. This is similar to when a message come from a room. But this `iFlyChatMessage` object contains a specific url string as a message string of the file that is sent to iFlyChatLibrary. Now you can download/view the file content from this url as you want in your app. To get this `iFlyChatMessage` object in your application, receive the intent with intent action named `iFlyChat.onMessagefromUser`.

```
if (intent.getAction().equals("iFlyChat.onMessageFromRoom")) {
    iFlyChatMessage messageObject = intent.getParcelableExtra("messsageObj");
}
```
