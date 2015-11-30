###Receiving Global List

iFlyChatLibrary polls every 2 mins to the server to get the updated user and room list, together which we call as Global list or Roster. Whenever the iFlyChatLibrary gets the global list from the server, it `sendBroadcast` with `iFlyChatRoster` object and intent filter action `iFlyChat.onGlobalListUpdate`. Therefore, it is required that the application must listen to this broadcast in order to receive the updated global list form the server and render it in the view.

To get a `iFlyChatRoster` object from this broadcast and receive the updated global list. The user needs to check for corresponding intent action and retrieve the `iFlyChatRoster` object :

* Match the intent action in your `onReceive()` method.
```
    if (intent.getAction().equals("iFlyChat.onGlobalListUpdate")) {
    
        iFlyChatRoster roster = intent.getParcelableExtra("globalList");
        LinkedHashMap<String,iFlyChatUser> users = roster.getUserList();
        LinkedHashMap<String,iFlyChatRoom> rooms = roster.getRoomList();
        
        for (Map.Entry<String, iFlyChatUser> entry : users.entrySet()) {
            iFlyChatUser userObj = entry.getValue();
        }
        for (Map.Entry<String, iFlyChatRoom> entry : rooms.entrySet()) {
            iFlyChatRoom roomObj = entry.getValue();
        }
        
    }
```
<br>

You can get updated `iFlyChatRoster` object from which you can get updated users and rooms `LinkedHashMap` by calling corresponding getter methods. You can get a single user and a room object from the users and rooms `LinkedHashMap` objects by running a for loop and doing `getValue()`.
