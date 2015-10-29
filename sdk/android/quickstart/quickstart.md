**Steps to integrate iFlyChatLibrary to Android project**



1. Download the iFlyChatLibrary.jar file from the above link.
2. Open your Android studio project.
3. Look for libs folder in your app module. If the libs folder is not there then create libs folder in app module.
4. Copy and paste iFlyChatLibrary.jar file in the libs folder.
5. Right click on iFlyChatLibrary.jar file in Android Studio and click on “Add as Library”.
6. To start the chat, we need to initialize the activity. In your activity’s onCreate() method :

    * Create and Initialize a LocalBroadcastManager object.
<code>
LocalBroadcastManager bManager = LocalBroadcastManager.getInstance(this);
</code>

    * Call setiFlyChatContext(Context) method of Utilities class in iFlyChatLibrary and give your application context object to this class.
<code>
Utilities.setiFlyChatContext(getApplicationContext());
</code>

    * If Session Key is not available then, Create and initialize the iFlyChatUserSession object with your username and password.
<code>
iFlyChatUserSession userSession = new iFlyChatUserSession("your_username", "your_password");
</code>

    * If Session Key is available then, Create and initialize the iFlyChatUserSession object with your username, password and sessionKey.
<code>
iFlyChatUserSession userSession = new iFlyChatUserSession("your_username", "your_password", “your_sessionKey”);
</code>


Create and initialize the iFlyChatConfig object. Use the serverHost and authUrl provided by iFlyChat.
<code>
iFlyChatConfig config = new iFlyChatConfig(serverHost, authUrl, isHttps);
</code>

- Create and initialize the iFlyChatUserAuthService object.
<code>
iFlyChatUserAuthService authService = new iFlyChatUserAuthService(config, userSession);
</code>

- Get sessionKey from userSession object.
<code>
String sessionKey = userSession.getSessionKey();
</code>

- Create and initialize the iFlyChatService object.
<code>
iFlyChatService service = new iFlyChatService(userSession, config, authService);
</code>

- Connect the chat using sessionKey.
<code>
service.connectChat(sessionKey);
</code>

1. In your activity’s onStart() method :

    * Create and Initialize a IntentFilter object.
<code>
IntentFilter intentFilter = new IntentFilter();
</code>

    * Depending on the events you want to listen, you can add Actions to your intent filter. Following are some of the actions you can listen to.
<code>
intentFilter.addAction("iFlyChat.onChatConnect");
intentFilter.addAction("iFlyChat.onGlobalListUpdate");
intentFilter.addAction("iFlyChat.onMessageFromRoom");
intentFilter.addAction("iFlyChat.onMessageFromUser");
</code>

    * You need to register a receiver with the above intent filter to your broadcast manager object.
<code>
bManager.registerReceiver(bReceiver, intentFilter);
</code>

2. To send message to User

    * Create a new iFlyChatMessageObject (msg).
<code>
iFlyChatMessage msgObj = new iFlyChatMessage("", currentUser.getId(), currentUser.toId() , currentUser.getName(), currentUser.toName(), messageToUser_String , "", currentUser.getProfileUrl(), currentUser.getAvatarUrl(), currentUser.getRole(), "", "user"); 
</code>

    * Call sendMessageToUser(messageObject)
<code>
service.sendMessageToUser(msgObj);
</code>

3. To send message to Room
    * Create a new iFlyChatMessageObject (msg).
<code>
iFlyChatMessage msgObj = new iFlyChatMessage("", currentUser.getId(), currentUser.toId(), currentUser.getName(), currentUser.toName() , messageToRoom_String, "", currentUser.getProfileUrl(), currentUser.getAvatarUrl(), currentUser.getRole(), "", "room"); 
</code>

    * Call sendMessageToRoom(messageObject)
<code>
service.sendMessageToRoom(msgObj);
</code>

4. To receive events from server. Create and initialize your receiver object and call onReceive() method.
<code>
private BroadcastReceiver bReceiver = new BroadcastReceiver() {
    @Override
    public void onReceive(Context context, Intent intent) {
}};
</code>

5. To receive event(iFlyChat.onMessageFromUser) corresponding to your action of sendMessageToUser. Match the intent action in your onReceive() method. If matched then you will get corresponding iFlyChatMessage object.
<code>
if (intent.getAction().equals("iFlyChat.onMessageFromUser")) {
    message = intent.getParcelableExtra("messageObj");
}
</code>

6. To receive event(iFlyChat.onMessageFromRoom) corresponding to your action of sendMessageToRoom. Match the intent action in your onReceive() method. If matched then you will get corresponding iFlyChatMessage object.
<code>
if (intent.getAction().equals("iFlyChat.onMessageFromRoom")) {
    message = intent.getParcelableExtra("messageObj");
}
</code>

7. Unregister your broadcast Receiver in the onStop() method of your activity.
<code>
@Override
protected void onStop() {
    super.onStop();
    bManager.unregisterReceiver(bReceiver);
}
</code>

8. Disconnect chat whenever the application is terminated. This can be done in your activity’s onDestroy() method by calling disconnectChat() method of service object.
<code>
@Override
protected void onDestroy(){
    service.disconnectChat();
    super.onDestroy();
}
</code>
