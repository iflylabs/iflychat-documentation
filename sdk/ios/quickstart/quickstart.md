#Installation & Setup#

1. Copy the `iFlyChatLibrary.framework` file from the above link to your project. To do this, you just need to drag and drop the file to your project.


    ![Add iFlyChat Framework file](https://iflychat-website-iflylabs.netdna-ssl.com/sites/default/files/docs/sdk/ios/adding-iFlyChatLibrary-framework-file-documentation.gif)


2. Add `libicucore.tbd` file to your project.
    * Go to your application's target.
    * Go to `"General"` tab.
    * Under `"Linked frameworks and libraries"` add the above libraries using the plus button.

    ![Add libicucore.tbd file to project](https://iflychat-website-iflylabs.netdna-ssl.com/sites/default/files/docs/sdk/ios/adding-library-to-iFlyChat-example-application-documentation.gif)  
  
3. Import the `“iFlyChatLibrary/iFlyChatlibrary.h”` file wherever you want to use the chat service functions.

    ~~~
    #import "iFlyChatLibrary/iFlyChatLibrary.h"
    ~~~
    Note: In a Swift iOS project, one will need to create an Objective-C bridging header to be able to import the framework's header file.

       * Create an Objective-C header file in your project and import the `iFlyChatLibrary.h` file there.


       * Add the relative path of this header file in the `"Build Settings"` of your project's target under `Objective-C Bridging Header` option.

           ![Adding relative path to build settings](https://iflychat-website-iflylabs.netdna-ssl.com/sites/default/files/docs/sdk/ios/adding-bridging-header-setting-documentation.gif)

##Precautions to be taken.

1. Make sure that in your application target's `Build Settings`, under `"Framework Search Path"`, the framework's path is mentioned. To avoid any problem, it is recommended to copy the framework file while linking.

2. iOS 9's `App Transport Security` does not allow for "http" connections. To work around it, you may add an exception in the `Info.plist` file in the main <dict> tag like so:

    ~~~xml
    <key>NSAppTransportSecurity&lt;/key>  
    <dict>  
          <key>NSAllowsArbitraryLoads</key>  
          <false/>  
           <key>NSExceptionDomains</key>  
           <dict>  
                <key>yourdomain.com</key>  
                <dict>  
                    <key>NSIncludesSubdomains</key>  
                    <true/>  
                    <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>  
                    <true/>  
                    <key>NSTemporaryExceptionMinimumTLSVersion</key>  
                    <string>TLSv1.1</string>  
                </dict>  
           </dict>  
    </dict>
    ~~~

    or if you need to allow all "http" connections, you may write the following code:

    ~~~xml
    <key>NSAppTransportSecurity&lt;/key>  
         <dict>  
              <key>NSAllowsArbitraryLoads</key><true/>  
         </dict>
    ~~~
  
3. Set `"ENABLE_BITCODE"` to NO in Application target's `Build Settings` when testing on a device.


#Chat Initialization, connection and disconnection


iFlyChatLibrary uses NSNotification to pass data from the library to the application. Therefore, it is required by the user to add observers for the notifications and remove them when not needed. Observers can be added in view controller's `"viewWillAppear"` method while observers can be removed in `"viewDidDisasppear"` method.


##Initialization and connection  
Follow the steps below to intialize the chat

1. Create and initialize the `iFlyChatUserSession` object.

    ~~~
    //OBJECTIVE-C

    iFlyChatUserSession *session = [[iFlyChatUserSession alloc] initIFlyChatUserSessionwithUserName:@"prateek" userPassword:@"password" userSessionKey:@"sessionkey if available otherwise empty string"];
    ~~~

    ~~~
    //SWIFT

    var session: iFlyChatUserSession = iFlyChatUserSession(IFlyChatUserSessionwithUserName: "prateek", userPassword: "password", userSessionKey: "sessionkey if available otherwise empty string")
    ~~~

    >`UserName` and `userPassword` are the two sufficient parameters required by iFlyChat to authenticate the user and get the session key from the server. These parameters are to be taken from the user through the user interface.

    >The `sessionKey` is a unique key that iFlyChat server generates for every user that is authenticated on the server. The validity for the session key is 12 hours so if the user has access to the old session key, it can be passed while creating an object of `iFlyChatUserSession` class. This session key will then be used while connecting to the chat in later steps.


2. Create and initialize the `iFlyChatConfig` object

    ~~~
    //OBJECTIVE-C

    iFlyChatConfig *config = [[iFlyChatConfig alloc] initIFlyChatConfigwithServerHost:@"example.com" authUrl:@"authenticate/the/user.com" isHttps:YES];
    ~~~

    ~~~
    //SWIFT

    var config: iFlyChatConfig = iFlyChatConfig(IFlyChatConfigwithServerHost: "example.com", authUrl: "authenticate/the/user.com")
    ~~~
  
    >`Server host` is the URL string provided to the user by iFlyChat when the user signs up for the service. This is the key element through which the client connects to the iFlyChat server.

    >`Auth URL` is the URL string provided by iFlyChat when the user signs up for the service. This is used when the client needs to authenticate the user on iFlyChat servers.

    >`isHttps` is the boolean that denotes if the connection should be secure or not.

    >This class also fetches the iFlyChat settings from the server using the session key.


3. Set the `"AutoReconnect"` parameter of the `iFlyChatConfig` object to whatever to you want to. Default is "YES" or true.

    ~~~
    OBJECTIVE-C

    [config setAutoReconnect:YES];  
    ~~~

    ~~~
    //SWIFT

    config.setAutoReconnect(true)
    ~~~
  
    >This BOOL value is set after `iFlyChatConfig` object is created. By default it is set to "YES" or true. This value specifies whether the client should attempt a reconnect in case the connection is broken if an invalid session key is supplied while creating `iFlyChatUserSession` object or due to some network or server error. There is a hard coded limit on the number of times reconnection will be attempted and that is equal to 10.


4. Create and initialize the `iFlyChatUserAuthService` object

    ~~~
    //OBJECTIVE-C

    iFlyChatUserAuthService *authService = [[iFlyChatUserAuthService alloc] initIFlyChatUserAuthServiceWithConfig:config userSession:session];
    ~~~

    ~~~
    //SWIFT

    var authService: iFlyChatUserAuthService = iFlyChatUserAuthService(IFlyChatUserAuthServiceWithConfig: config, userSession: session)
    ~~~
  
    >The object of this class stores the `iFlyChatUserSession` and `iFlyChatConfig` objects created above at one place. Therefore, it is necessary to create those objects first before creating an object for this class.

    >The class also checks if the session key is present in `iFlyChatUserSession` object or not. If it is not present there, it uses its own public function `"getNewSessionKey"` to authenticate the user and gets the session key from iFlyChat servers using the `username` and `userpassword` from `iFlyChatUserSession` object and `Auth URL` from `iFlyChatConfig` object.

    >After getting the session key, it gives out a NSNotification with identifier/name `"iFlyChat.onUserAuthSuccess"` and session key string object, listening to which the user can save the session key in the database to be used when the user connects to the chat next time.


5. Get `iFlyChatSettings` using `iFlyChatConfig` object

    ~~~
    //OBJECTIVE-C

    [config getiFlyChatSettingsUsingSessionKey:<sessionkey>];
    ~~~

    ~~~
    //SWIFT

    config.getiFlyChatSettingsUsingSessionKey(<sessionkey>)
    ~~~


6. Create and initialize `iFlyChatService` object.

    ~~~
    //OBJECTIVE-C

    iFlyChatService *service = [[iFlyChatService alloc] initIFlyChatServicewithConfig:config session:session userAuthService:authService];
    ~~~

    ~~~
    //SWIFT

    service = iFlyChatService(IFlyChatServicewithConfig: config, session: session, userAuthService: authService)
    ~~~
  
    >The object of this class performs all the core functions of iFlyChat. While initializing it requires `iFlyChatConfig`, `iFlyChatUserSession` and `iFlyChatUserAuthService` objects created above. Therefore, it is necessary to create those objects first before creating the object for this class.


7. Connect the chat

    ~~~
    //OBJECTIVE-C

    [service connectChat];
    ~~~
    
    ~~~
    //SWIFT

    service.connectChat()
    ~~~
  
    >This function initiates the process of connecting the client to iFlyChat chat servers. It checks for the session key validity while connecting and if it is invalid and auto reconnect (see above: `iFlyChatConfig`) value is set to "YES", then it automatically retrieves a new session key from the server and connects the chat. 

    >After the chat is connected to the server, iFlyChatLibrary will throw a NSNotification with a dictionary of user's details as `iFlyChatUser` object with key `"iFlyChatCurrentUser"` and session key used to connect to the chat. with key `"sessionKey"`. The notification name would be `"iFlyChat.onChatConnect"`. 


8. To listen to `"iFlyChat.onChatConnect"` event, the user needs to add the observer for this notification and retrieve the `iFlyChatUser` object and session key string from the notification object.

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onChatConnect:) name:@”iFlyChat.onChatConnect” object:nil];  

    -(void) onChatConnect:(NSNotification *)notification  
    {  
        id object = [notification object];  
        iFlyChatUser *currentUser = [object objectForKey:@"iFlyChatCurrentUser"];  
        NSString *sessionKey = [object objectForKey:@"sessionKey"];  
    }  
    ~~~

    ~~~
    //SWIFT

    NSNotificationCenter.defaultCenter().addObserver  
    (  
        self,  
        selector: "onChatConnect:",  
        name: "iFlyChat.onChatConnect",  
        object: nil  
    )  

    func onChatConnect(notification: NSNotification)  
    {  
        let object:AnyObject = notification.object!  
        if let authSuccess = object as? NSDictionary  
        {  
            var currentUser: iFlyChatUser = authSuccess.objectForKey("iFlyChatCurrentUser") as! iFlyChatUser  
            var skey: String = object.objectForKey("sessionKey") as! String  
        }  
    }  
    ~~~

##Disconnection

1. To disconnect the chat, the user needs to call the following function of the `iFlyChatService` object

    ~~~
    //OBJECTIVE-C

    [service disconnectChat];
    ~~~

    ~~~
    //SWIFT

    service.disconnectChat()
    ~~~
  
    >Along with calling this function, the user needs to remove the NSNotification observers for clean disconnection.

    >The disconnection method must also be called when the app terminates, i.e., in the app delegate. This will ensure clean closure of the connection of the client to the server and iFlyChatLibrary to the UI of the application.


    >After the chat is disconnected from the server, iFlyChatLibrary will throw a NSNotification name `"iFlyChat.onChatDisconnect"` to allow the users to perform final clean up. 

    To listen to `"iFlyChat.onChatDisconnect"` event, the user needs to add the observer for this notification.

    ~~~
    //OBJECTIVE-C  

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onChatDisconnect:) name:@”iFlyChat.onChatDisconnect” object:nil];  

    -(void) onChatDisconnect:(NSNotification *)notification  
    {  
        //perform  your clean up   
    }  
    ~~~

    ~~~
    //SWIFT

    NSNotificationCenter.defaultCenter().addObserver  
    (  
        self,  
        selector: "onChatDisconnect:",  
        name: "iFlyChat.onChatDisconnect",  
        object: nil  
    )  

    func onChatDisconnect(notification: NSNotification)  
    {  
        //perform your operation  
    }  
    ~~~

#Sending and receiving messages


1. Send message to user

    To send a message to user, the first person needs to create an object of `iFlyChatMessage` object with the required parameters and pass that object to the `iFlyChatService` object's method `"sendMessagetoUser"`:

    ~~~
    //OBJECTIVE-C

    iFlyChatMessage *msg = [[iFlyChatMessage alloc] initIFlyChatMessageObjectwithMessage:@"Message for User" fromName:@”John” toName:@"Prateek" fromId:@"1" toId:@"2" message_id:@"" color:@"" fromProfileUrl:@"" fromAvatarUrl:@"" fromRole:@"" time:@"", type:@"user"];​

    [service sendMessagetoUser:msg];
    ~~~

    ~~~
    //SWIFT

    var msg: iFlyChatMessage = iFlyChatMessage(IFlyChatMessageObjectwithMessage: "Message for user", fromName: "John", toName: "Prateek", fromId: "1", toId: "2", message_id: "", color: "", fromProfileUrl: "", fromAvatarUrl: "", fromRole: "", time: "", type: "user")

    service.sendMessagetoUser(msg)
    ~~~
  
    >`Message text`, `fromName`, `toName`, `fromId` and `toId` are the required parameters to create this message object otherwise the class will throw an exception.

    >The user should leave the `message_id` and `time` fields as empty strings because the iFlyChatLibrary itself creates those parameters and insert them into the final message that is sent to the server.

    >`color`, `fromProfileUrl`, `fromAvatarUrl` and `fromRole` are some of the optional parameters and can be left empty if not available.

    >`type` specifies whether the message object being created is for room or user.


2. Send message to room

    To send a message to room, the first person needs to create an object of `iFlyChatMessage` object with the required parameters and pass that object to the `iFlyChatService` object's method `"sendMessagetoRoom"`:

    ~~~
    //OBJECTIVE-C

    iFlyChatMessage *msg = [[iFlyChatMessage alloc] initIFlyChatMessageObjectwithMessage:@"Message for Room" fromName:@”John” toName:@"Public Chatroom" fromId:@"1" toId:@"0" message_id:@"" color:@"" fromProfileUrl:@"" fromAvatarUrl:@"" fromRole:@"" time:@"", type:@"room"];​

    [service sendMessagetoRoom:msg];
    ~~~

    ~~~
    //SWIFT

    let msg: iFlyChatMessage = iFlyChatMessage(IFlyChatMessageObjectwithMessage: "Message for Room", fromName: "John", toName: "Public Chatroom", fromId: "1", toId: "0", message_id: "", color: "", fromProfileUrl: "", fromAvatarUrl: "", fromRole: "", time: "", type:"room")

    service.sendMessagetoRoom(msg)
    ~~~
  
    >`Message text`, `fromName`, `toName`, `fromId` and `toId` are the required parameters to create this message object otherwise the class will throw an exception.

    >The user should leave the `message_id` and `time` fields as empty strings because the iFlyChatLibrary itself creates those parameters and insert them into the final message that is sent to the server.

    >`color`, `fromProfileUrl`, `fromAvatarUrl` and `fromRole` are some of the optional parameters and can be left empty if not available.

    >`type` specifies whether the message object being created is for room or user.


3. Receiving message from user

    When some other user sends a message to the first user, iFlyChatLibrary throws a NSNotification with the `iFlyChatMessage` object and name `"iFlyChat.onMessagefromUser"`. Therefore, it is required that the application must listen to this notification in order to receive the message from the user and then the user can process the message.

    To listen to this notification and receive the message, the user needs to add observer to the application and retrieve the `iFlyChatMessage` object from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(receiveMessage:) name:@”iFlyChat.onMessagefromUser” object:nil];

    -(void) receiveMessage:(NSNotification *)notification
    {
        iFlyChatMessage *msg = [notification object];
    }
    ~~~

    ~~~
    //SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "receiveMessage:",
        name: "iFlyChat.onMessagefromUser",
        object: nil
    )

    func receiveMessage(notification: NSNotification)
    {
        let msg: iFlyChatMessage = notification.object! as! iFlyChatMessage
    }
    ~~~
  
4. Receiving message from room

    When some other room sends a message to the user, iFlyChatLibrary throws a NSNotification with the `iFlyChatMessage` object and name `"iFlyChat.onMessagefromRoom"`. Therefore, it is required that the application must listen to this notification in order to receive the message from the room and then the user can process the message.

    To listen to this notification and receive the message, the user needs to add observer to the application and retrieve the `iFlyChatMessage` object from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(receiveMessage:) name:@”iFlyChat.onMessagefromRoom” object:nil];

    -(void) receiveMessage:(NSNotification *)notification
    {
        iFlyChatMessage *msg = [notification object];
    }
    ~~~

    ~~~
    //SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "receiveMessage:",
        name: "iFlyChat.onMessagefromRoom",
        object: nil
    )

    func receiveMessage(notification: NSNotification)
    {
        let msg: iFlyChatMessage = notification.object! as! iFlyChatMessage
    }
    ~~~
  
5. Receiving Global List

    iFlyChatLibrary polls every 2 min to the server to get the updated user and room list, together which we call as Global list or Roster. Whenever the iFlyChatLibrary gets the global list from the server, it throws a NSNotification with `iFlyChatRoster` object and name `"iFlyChat.onGlobalListUpdate"`. Therefore, it is required that the application must listen to this notification in order to receive the updated global list form the server and render it in the view.

    To listen to this notification and receive the updated global list, the user needs to add observer to the application and retrieve the `iFlyChatRoster` object from the notification:

    ~~~
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(receiveGlobalList:) name:@”iFlyChat.onGlobalListUpdate” object:nil];

    -(void) receiveGlobalList:(NSNotification *)notification
    {
        iFlyChatRoster *updatedRoster = [notification object];
        //Now here, you can get userList and roomList separately by calling
        iFlyChatOrderedDictionary *userList = [updatedRoster getUserList];
        iFlyChatOrderedDictionary *roomList = [updatedRoster getRoomLIst];
    }
    ~~~
    
    ~~~
    //SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "receiveGlobalList:",
        name: "iFlyChat.onGlobalListUpdate",
        object: nil
    )

    func receiveGlobalList(notification: NSNotification)
    {
        var userlist: iFlyChatOrderedDictionary
        var roomlist: iFlyChatOrderedDictionary

        let object: AnyObject = notification.object!

        if let rosterItem = object as? iFlyChatRoster
        {
            //Now here, you can get userList and roomList separately by calling
            userlist = object.getUserList() 
            roomlist = object.getRoomList()
        }
    }
    ~~~
  
    Here, the `iFlyChatRoster` object actually returns two `iFlyChatOrderedDictionary` objects, one for `Userlist` and the other for `Roomlist`. These data structure types can be retrieved from the iFlyChatRoster object using the getter functions provided in the same. 

    To render userlist and roomlist in a tableview, it is required that the data source be an array. Therefore, we have made this custom data structure that provides the functionality of a dictionary and an array together.