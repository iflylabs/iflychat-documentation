**Steps to integrate iFlyChatLibrary to Android project**



1. Download the `iFlyChatLibrary.jar` file from the above link.
2. Open your Android studio project.
3. Look for libs folder in your `app` module. If the `libs` folder is not there then create `libs` folder in `app` module.
4. Copy and paste `iFlyChatLibrary.jar` file in the `libs` folder.
5. Right click on `iFlyChatLibrary.jar` file in Android Studio and click on `Add as Library`.
6. To start the chat, we need to initialize the activity. In your activity’s `onCreate()` method :
   * Create and Initialize a `LocalBroadcastManager` object.
   ~~~ {.language-java}
   LocalBroadcastManager bManager = LocalBroadcastManager.getInstance(this);
   ~~~
   * Call `setiFlyChatContext(Context)` method of `iFlyChatUtilities` class in iFlyChatLibrary and give your application context object to this class.
   ~~~ {.language-java}
   iFlyChatUtilities.setiFlyChatContext(getApplicationContext());
   ~~~
   * If Session Key is not available then, Create and initialize the `iFlyChatUserSession` object with your username and password.
   ~~~ {.language-java}
   iFlyChatUserSession userSession = new iFlyChatUserSession("your_username", "your_password");
   ~~~
   * If Session Key is available then, Create and initialize the `iFlyChatUserSession` object with your username, password and session key.
   ~~~ {.language-java}
   iFlyChatUserSession userSession = new iFlyChatUserSession("your_username", "your_password", “your_sessionKey”);
   ~~~


Create and initialize the `iFlyChatConfig` object. Use the `serverHost` and `authUrl` provided by iFlyChat.
~~~ {.language-java}
iFlyChatConfig config = new iFlyChatConfig(serverHost, authUrl, isHttps);
~~~
   - Create and initialize the `iFlyChatUserAuthService` object.
   ~~~ {.language-java}
   iFlyChatUserAuthService authService = new iFlyChatUserAuthService(config, userSession);
   ~~~
   - Get sessionKey from `userSession` object.
   ~~~ {.language-java}
   String sessionKey = userSession.getSessionKey();
   ~~~
   - Create and initialize the `iFlyChatService` object.
   ~~~ {.language-java}
   iFlyChatService service = new iFlyChatService(userSession, config, authService);
   ~~~
   - Connect the chat using `sessionKey`.
   ~~~ {.language-java}
   service.connectChat(sessionKey);
   ~~~

1. In your activity’s `onStart()` method :
   - Create and Initialize a `IntentFilter` object.
    ~~~ {.language-java}
    IntentFilter intentFilter = new IntentFilter();
    ~~~
   - Depending on the events you want to listen, you can add Actions to your intent filter. Following are some of the actions you can listen to.
    ~~~ {.language-java}
    intentFilter.addAction("iFlyChat.onChatConnect");
    intentFilter.addAction("iFlyChat.onGlobalListUpdate");
    intentFilter.addAction("iFlyChat.onMessageFromRoom");
    intentFilter.addAction("iFlyChat.onMessageFromUser");
    ~~~
   - You need to register a receiver with the above intent filter to your broadcast manager object `bManager`.
    ~~~ {.language-java}
    bManager.registerReceiver(bReceiver, intentFilter);
    ~~~

2. To send message to User
  * Create a new `iFlyChatMessageObject` `msg`.
    ~~~ {.language-java}
    iFlyChatMessage msgObj = new iFlyChatMessage("", currentUser.getId(), currentUser.toId() , currentUser.getName(),    currentUser.toName(), messageToUser_String , "", currentUser.getProfileUrl(),              currentUser.getAvatarUrl(),          currentUser.getRole(), "", "user"); 
    ~~~
  * Call `sendMessageToUser(messageObject)`
    ~~~ {.language-java}
    service.sendMessageToUser(msgObj);
    ~~~

3. To send message to Room
  * Create a new `iFlyChatMessageObject` `msg`.
    ~~~ {.language-java}
    iFlyChatMessage msgObj = new iFlyChatMessage("", currentUser.getId(), currentUser.toId(), currentUser.getName(),    currentUser.toName() , messageToRoom_String, "", currentUser.getProfileUrl(), currentUser.getAvatarUrl(),          currentUser.getRole(), "", "room"); 
    ~~~
  * Call `sendMessageToRoom(messageObject)`
    ~~~ {.language-java}
    service.sendMessageToRoom(msgObj);
    ~~~

4. To receive events from server. Create and initialize your receiver object and call `onReceive()` method.
  ~~~
  private BroadcastReceiver bReceiver = new BroadcastReceiver() {
      @Override
      public void onReceive(Context context, Intent intent) {
  }};
  ~~~

5. To receive event `iFlyChat.onMessageFromUser` corresponding to your action of `sendMessageToUser`. Match the intent action in your `onReceive()` method. If matched then you will get corresponding `iFlyChatMessage` object.
  ~~~ {.language-java}
  if (intent.getAction().equals("iFlyChat.onMessageFromUser")) {
      message = intent.getParcelableExtra("messageObj");
  }
  ~~~

6. To receive event `iFlyChat.onMessageFromRoom` corresponding to your action of `sendMessageToRoom`. Match the intent action in your `onReceive()` method. If matched then you will get corresponding `iFlyChatMessage` object.
  ~~~ {.language-java}
  if (intent.getAction().equals("iFlyChat.onMessageFromRoom")) {
      message = intent.getParcelableExtra("messageObj");
  }
  ~~~

7. Unregister your broadcast Receiver in the `onStop()` method of your activity.
  ~~~ {.language-java}
  @Override
  protected void onStop() {
      super.onStop();
      bManager.unregisterReceiver(bReceiver);
  }
  ~~~

8. Disconnect chat whenever the application is terminated. This can be done in your activity’s `onDestroy()` method by calling `disconnectChat()` method of service object.
  ~~~ {.language-java}
  @Override
  protected void onDestroy(){
      service.disconnectChat();
      super.onDestroy();
  }
  ~~~
