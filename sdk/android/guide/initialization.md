###Chat Initialization, Connection and Disconnection



To start the chat, we need to initialize the activity. In your activity’s `onCreate()` method :

* Create and Initialize a `LocalBroadcastManager` object.
    ~~~ {.language-java}
    LocalBroadcastManager bManager = LocalBroadcastManager.getInstance(this);
    ~~~
<br>
Create the `LocalBroadcastManager` object outside `onCreate()` method. It will make it accessible throughout the activity. Also it will be useful in unregistering receivers in `onStop()` method. Initialize `bManager` object with the current activity instance in onCreate() method.


* Call setiFlyChatContext(Context) method of `iFlyChatUtilities` class in iFlyChatLibrary and give your application context object to this class.
    ~~~ {.language-java}
    iFlyChatUtilities.setiFlyChatContext(getApplicationContext());
    ~~~
<br>

* If Session Key is not available then, create and initialize the `iFlyChatUserSession` object with your username and password.
    ~~~ {.language-java}
    iFlyChatUserSession userSession = new iFlyChatUserSession("your_username", "your_password");
    ~~~
<br>

* If Session Key is available then, create and initialize the `iFlyChatUserSession` object with your username, password and sessionKey.
    ~~~ {.language-java}
    iFlyChatUserSession userSession = new iFlyChatUserSession("your_username", "your_password", “your_sessionKey”);
    ~~~
<br>

User name and user password are the two sufficient parameters required by iFlyChat to authenticate the user and get the session key from the server. These parameters are to be taken from the user through the user interface.

The session key is a unique key that iFlyChat server generates for every user that is authenticated on the server. The validity for the session key is 12 hours so if the user has access to the old session key, it can be passed while creating an object of `iFlyChatUserSession` class. This session key will then be used while connecting to the chat in later steps.

<br>

* Create and initialize the `iFlyChatConfig` object. Use the `serverHost` and `authUrl` provided by iFlyChat.
    ~~~ {.language-java}
    iFlyChatConfig config = new iFlyChatConfig(serverHost, authUrl, isHttps);
    ~~~
<br>

`serverHost` is the URL string provided to the user by iFlyChat when the user signs up for the service. This is the key element through which the client connects to the iFlyChat server.

`authUrl` is the URL string provided by iFlyChat when the user signs up for the service. This is used when the client needs to authenticate the user on iFlyChat servers.

`isHttps` is a boolean variable which tells iFlyChat whether your chat connection is secure or not. To make your chat connection secure set it to true otherwise false.

<br>
* Set the `AutoReconnect` parameter of the `iFlyChatConfig` object to whatever(true or false) to you want to. Default is true.
    ~~~ {.language-java}
    config.setAutoReconnect(true);
    ~~~
<br>

This boolean value is set after `iFlyChatConfig` object is created. By default it is set to true. This value specifies whether the client should attempt a reconnect in case the connection is broken if an invalid session key is supplied while creating `iFlyChatUserSession` object or due to some network or server error.

<br>
* Create and initialize the `iFlyChatUserAuthService` object.
    ~~~ {.language-java}
    iFlyChatUserAuthService authService = new iFlyChatUserAuthService(config, userSession);
    ~~~
<br>

The object of this class stores the `iFlyChatConfig` and `iFlyChatUserSession` objects created above at one place. Therefore, it is necessary to create those objects first before creating an object for this class.

The class also checks if the session key is present in `iFlyChatUserSession` object or not. If it is not present there, it uses its own public function `getNewSessionKey` to authenticate the user and gets the session key from iFlyChat servers using the username and userpassword from `iFlyChatUserSession` object and Auth URL from `iFlyChatConfig` object.

After getting the session key, it sends a broadcast intent with action `iFlyChat.onUserAuthSuccess` and session key String object, listening to which, the user can save the session key in the database to be used when the user connects to the chat next time.

<br>

* Get sessionKey from `userSession` object.
    ~~~ {.language-java}
    String sessionKey = userSession.getSessionKey();
    ~~~
<br>

Get session key from calling `getSessionKey()` method and store in a string sessionKey. This will be used below in calling `connectChat(sessionKey)` method of `iFlyChatService` object.

<br>

* Create and initialize the `iFlyChatService` object.
    ~~~ {.language-java}
    iFlyChatService service = new iFlyChatService(userSession, config, authService);
    ~~~
<br>

The object of this class performs all the core functions of iFlyChat. While initializing it requires `iFlyChatConfig`, `iFlyChatUserSession` and `iFlyChatUserAuthService` objects created above. Therefore, it is necessary to create those objects first before creating the object for this class.

<br>

* Connect the chat using sessionKey.
    ~~~ {.language-java}
    service.connectChat(sessionKey);
    ~~~
<br>

This function initiates the process of connecting the client to iflychat chat servers. It checks for the session key validity while connecting and if it is invalid and auto reconnect (see above: `iFlyChatConfig`) value is set to "YES", then it automatically retrieves a new session key from the server and connects the chat.

<br>

* Create and initialize your receiver object and call `onReceive()` method in your activity.

    ~~~ {.language-java}
    private BroadcastReceiver bReceiver = new BroadcastReceiver() 
    {
        @Override
        public void onReceive(Context context, Intent intent) 
        {
        }
    };
    ~~~
<br>

Whenever some message comes from the server. The `iFlyChatService` class will get the data first. It will define a intent with corresponding intent action and `sendBroadcast` with a string/object. To receive events from a server in your activity `BroadcastManager` object will be used.

The bReceiver object of the `BroadcastReceiver` type is used to register the receiver with `BroadcastManager` object. 

`onReceive()` method will be used to match the intent actions(defined in `onStart()` method) and perform operations on the events recieved in this from the server.

<br>

In your activity’s `onStart()` method :

* Create and Initialize a `IntentFilter` object.
    ~~~ {.language-java}
    IntentFilter intentFilter = new IntentFilter();
    ~~~
<br>

The `intentFilter` object of the `IntentFilter` type is used to register the intentFilter with `BroadcastManager` object.

<br>

* Depending on the events you want to listen, you can add actions to your intent filter in `onStart()` method. Following are all the actions you can listen to:
    ~~~ {.language-java}
    intentFilter.addAction("iFlyChat.onUserSessionAuthSuccess");
    intentFilter.addAction("iFlyChat.onChatConnect");
    intentFilter.addAction("iFlyChat.onGetSessionKey");
    intentFilter.addAction("iFlyChat.onGlobalListUpdate");
    intentFilter.addAction("iFlyChat.onMessageFromRoom");
    intentFilter.addAction("iFlyChat.onMessageFromUser");
    intentFilter.addAction("iFlyChat.onUserKick");
    intentFilter.addAction("iFlyChat.onUserBan");
    intentFilter.addAction("iFlyChat.onUserBanIp");
    intentFilter.addAction("iFlyChat.onMessageDeleteFromRoom");
    intentFilter.addAction("iFlyChat.onMessageDeleteFromUser");
    intentFilter.addAction("iFlyChat.onRoomThreadHistoryClear");
    intentFilter.addAction("iFlyChat.onUserThreadHistoryClear");
    intentFilter.addAction("iFlyChat.onUserThreadHistory");
    intentFilter.addAction("iFlyChat.onRoomThreadHistory");
    intentFilter.addAction("iFlyChat.onUploadProgress");
    intentFilter.addAction("iFlyChat.onError");
    ~~~
<br>

In your activity you need to add actions in your `IntentFilter` object to distinguish these intents based on their intent actions. These intent actions are explained further in this document.

<br>

* Register receiver to listen all the broadcast send by `iFlyChatService` class.
    ~~~ {.language-java}
    object.bManager.registerReceiver(bReceiver, intentFilter);
    ~~~
<br>

To listen events, register a receiver with the above `bReceiver` object of BroadcastReceiver type and IntentFilter object `intentFilter` to your BroadcastManager object `bManager`. 

<br>

To get session key on event`iFlyChat.onUserSessionAuthSuccess`

* Match the intent action in your `onReceive()` method. Then do `getString("sessionKey")` on Bundle type object `bundleData`.
    ~~~ {.language-java}
    if (intent.getAction().equals("iFlyChat.onUserSessionAuthSuccess")) {
        Bundle bundleData = intent.getExtras();
        String sessionKey = bundleData.getString("sessionKey");
    }
    ~~~
<br>

This intent action `iFlyChat.onUserSessionAuthSuccess` is added to the intent, when your user is validated on the iFlyChat server. Then a new session Key is broadcasted from `iFlyChatUserAuthService` class. You can use this session key in the next login of the user to create and initialize the `iFlyChatUserSession` object with your username, password and sessionKey.

<br>

To get a current user object on event `iFlyChat.onChatConnect`

* Match the intent action in your `onReceive()` method. Then do `intent.getParcelableExtra("currentUser")` and save the result in `iFlyChatUser` object.
    ~~~ {.language-java}
    if (intent.getAction().equals("iFlyChat.onChatConnect")) {
        iFlyChatUser currentUser = intent.getParcelableExtra("currentUser");
    }
    ~~~
<br>

The above `iFlyChatUser` object `currentUser` is your apps, currently login user with authentication. There are several getter methods which gives you some properties of the current user. Which you can use to show in the UI. These getter methods are explained in the javadoc of the iFlyChatLibrary.

**Example:**

~~~ {.language-java}
Toast.makeText(context, "onChatConnect: "+currentUser.getId() + " " + currentUser.getName() + " " + currentUser.getRole()
                + " " + currentUser.getStatus() + " " + currentUser.getAvatarUrl() + " " + currentUser.getProfileUrl(),
        Toast.LENGTH_LONG).show();
~~~
<br>

**Disconnection**

Unregister your broadcast Receiver in the onStop() method of your activity.

~~~ {.language-java}
@Override
protected void onStop() 
{
    super.onStop();
    bManager.unregisterReceiver(bReceiver);
}
~~~
<br>

To disconnect the chat, the user first needs to unregister all the receivers attached to `BroadcastManager` object `bManager` in `onStop()` method of the activity. 

<br>

User needs to call the following function of the `iFlyChatService` object.
~~~ {.language-java}
@Override
protected void onDestroy()
{
    service.disconnectChat();
    super.onDestroy();
}
~~~
<br>

Disconnect chat whenever the application is terminated. This can be done in your activity’s `onDestroy()` method by calling `disconnectChat()` method of service object. Do not call this method if you are 
starting another activity and closing the current one. This will ensure clean closure of the connection of the client to the server and iFlyChatLibrary to the UI of the application.
