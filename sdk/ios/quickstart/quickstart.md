#Installation & Setup#

1. Copy the <font color='blue'>iFlyChatLibrary.framework</font> file from the above link to your project. To do this, you just need to drag and drop the file to your project.


    ![Add iFlyChat Framework file](https://lh5.googleusercontent.com/-6es2W67Wf7k/VgEhAewx7HI/AAAAAAAAA0w/mLWhUWTPfDw/w804-h540-no/Adding%2BiFlyChatLibrary%2BFramework%2Bfile.gif)


2. Add <font color='blue'>libicucore.tbd</font> file to your project.
    * Go to your application's target.
    * Go to <font color='blue'>"General"</font> tab.
    * Under <font color='blue'>"Linked frameworks and libraries"</font> add the above libraries using the plus button.

    ![Add libicucore.tbd file to project](https://lh3.googleusercontent.com/-Jf1cnedJjIA/VgEhAYg_ltI/AAAAAAAAA0w/K0shr0R0Gyc/w804-h540-no/Adding%2BLibrary%2Bto%2BiFlyChat%2BExample%2BApplication.gif)  
  
3. Import the <font color='blue'>“iFlyChatLibrary/iFlyChatlibrary.h”</font> file wherever you want to use the chat service functions.

    <code>
    #import "iFlyChatLibrary/iFlyChatLibrary.h"</code>  
    Note: In a Swift iOS project, one will need to create an Objective-C bridging header to be able to import the framework's header file.

       * Create an Objective-C header file in your project and import the <font color='blue'>iFlyChatLibrary.h</font> file there.


       * Add the relative path of this header file in the <font color='blue'>"Build Settings"</font> of your project's target under <font color='blue'>Objective-C Bridging Header</font> option.

           ![Adding relative path to build settings](https://lh3.googleusercontent.com/-4B-7-ONrNs8/VgEizogwXzI/AAAAAAAAA1M/trXPn3kHlVk/w804-h540-no/Adding%2BBridging%2BHeader%2BSetting.gif)

##Precautions to be taken.

1. Make sure that in your application target's <font color='blue'>Build Settings</font>, under <font color='blue'>"Framework Search Path"</font>, the framework's path is mentioned. To avoid any problem, it is recommended to copy the framework file while linking.

2. iOS 9's <font color='blue'>App Transport Security</font> does not allow for "http" connections. To work around it, you may add an exception in the <font color='blue'>Info.plist</font> file in the main <dict> tag like so:

    <code>
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
    

    or if you need to allow all "http" connections, you may write the following code:

    <key>NSAppTransportSecurity&lt;/key>  
         <dict>  
              <key>NSAllowsArbitraryLoads</key><true/>  
         </dict>
    </code>  
  
3. Set <font color='blue'>"ENABLE_BITCODE"</font> to NO in Application target's <font color='blue'>Build Settings</font> when testing on a device.


#Chat Initialization, connection and disconnection


iFlyChatLibrary uses NSNotification to pass data from the library to the application. Therefore, it is required by the user to add observers for the notifications and remove them when not needed. Observers can be added in view controller's <font color='blue'>"viewWillAppear"</font> method while observers can be removed in <font color='blue'>"viewDidDisasppear"</font> method.


##Initialization and connection  
Follow the steps below to intialize the chat

1. Create and initialize the <font color='blue'>iFlyChatUserSession</font> object.

    <code>
    OBJECTIVE-C

    iFlyChatUserSession *session = [[iFlyChatUserSession alloc] initIFlyChatUserSessionwithUserName:@"prateek" userPassword:@"password" userSessionKey:@"sessionkey if available otherwise empty string"];


    SWIFT

    var session: iFlyChatUserSession = iFlyChatUserSession(IFlyChatUserSessionwithUserName: "prateek", userPassword: "password", userSessionKey: "sessionkey if available otherwise empty string")
    </code>  
    <font color='blue'>UserName</font> and <font color='blue'>userPassword</font> are the two sufficient parameters required by iFlyChat to authenticate the user and get the session key from the server. These parameters are to be taken from the user through the user interface.

    The <font color='blue'>sessionKey</font> is a unique key that iFlyChat server generates for every user that is authenticated on the server. The validity for the session key is 12 hours so if the user has access to the old session key, it can be passed while creating an object of <font color='blue'>iFlyChatUserSession</font> class. This session key will then be used while connecting to the chat in later steps.


2. Create and initialize the <font color='blue'>iFlyChatConfig</font> object

    <code>
    OBJECTIVE-C

    iFlyChatConfig *config = [[iFlyChatConfig alloc] initIFlyChatConfigwithServerHost:@"example.com" authUrl:@"authenticate/the/user.com" isHttps:YES];


    SWIFT

    var config: iFlyChatConfig = iFlyChatConfig(IFlyChatConfigwithServerHost: "example.com", authUrl: "authenticate/the/user.com")
    </code>
  
    <font color='blue'>Server host</font> is the URL string provided to the user by iFlyChat when the user signs up for the service. This is the key element through which the client connects to the iFlyChat server.

    <font color='blue'>Auth URL</font> is the URL string provided by iFlyChat when the user signs up for the service. This is used when the client needs to authenticate the user on iFlyChat servers.

    <font color='blue'>isHttps</font> is the boolean that denotes if the connection should be secure or not.

    This class also fetches the iFlyChat settings from the server using the session key.


3. Set the <font color='blue'>"AutoReconnect"</font> parameter of the <font color='blue'>iFlyChatConfig</font> object to whatever to you want to. Default is "YES" or true.

    <code>
    OBJECTIVE-C

    [config setAutoReconnect:YES];  


    SWIFT

    config.setAutoReconnect(true)
    </code>
  
    This BOOL value is set after <font color='blue'>iFlyChatConfig</font> object is created. By default it is set to "YES" or true. This value specifies whether the client should attempt a reconnect in case the connection is broken if an invalid session key is supplied while creating <font color='blue'>iFlyChatUserSession</font> object or due to some network or server error. There is a hard coded limit on the number of times reconnection will be attempted and that is equal to 10.


4. Create and initialize the <font color='blue'>iFlyChatUserAuthService</font> object

    <code>
    OBJECTIVE-C

    iFlyChatUserAuthService *authService = [[iFlyChatUserAuthService alloc] initIFlyChatUserAuthServiceWithConfig:config userSession:session];


    SWIFT

    var authService: iFlyChatUserAuthService = iFlyChatUserAuthService(IFlyChatUserAuthServiceWithConfig: config, userSession: session)
    </code>
  
    The object of this class stores the <font color='blue'>iFlyChatUserSession</font> and <font color='blue'>iFlyChatConfig</font> objects created above at one place. Therefore, it is necessary to create those objects first before creating an object for this class.

    The class also checks if the session key is present in <font color='blue'>iFlyChatUserSession</font> object or not. If it is not present there, it uses its own public function <font color='blue'>"getNewSessionKey"</font> to authenticate the user and gets the session key from iFlyChat servers using the <font color='blue'>username</font> and <font color='blue'>userpassword</font> from <font color='blue'>iFlyChatUserSession</font> object and <font color='blue'>Auth URL</font> from <font color='blue'>iFlyChatConfig</font> object.

    After getting the session key, it gives out a NSNotification with identifier/name <font color='blue'>"iFlyChat.onUserAuthSuccess"</font> and session key string object, listening to which the user can save the session key in the database to be used when the user connects to the chat next time.


5. Get <font color='blue'>iFlyChatSettings</font> using <font color='blue'>iFlyChatConfig</font> object

    <code>
    OBJECTIVE-C

    [config getiFlyChatSettingsUsingSessionKey:<sessionkey>];


    SWIFT

    config.getiFlyChatSettingsUsingSessionKey(<sessionkey>)
    </code>  


6. Create and initialize <font color='blue'>iFlyChatService</font> object.

    <code>
    OBJECTIVE-C

    iFlyChatService *service = [[iFlyChatService alloc] initIFlyChatServicewithConfig:config session:session userAuthService:authService];


    SWIFT

    service = iFlyChatService(IFlyChatServicewithConfig: config, session: session, userAuthService: authService)
    </code>
  
    The object of this class performs all the core functions of iFlyChat. While initializing it requires <font color='blue'>iFlyChatConfig</font>, <font color='blue'>iFlyChatUserSession</font> and <font color='blue'>iFlyChatUserAuthService</font> objects created above. Therefore, it is necessary to create those objects first before creating the object for this class.


7. Connect the chat

    <code>
    OBJECTIVE-C

    [service connectChat];


    SWIFT

    service.connectChat()
    </code>
  
    This function initiates the process of connecting the client to iFlyChat chat servers. It checks for the session key validity while connecting and if it is invalid and auto reconnect (see above: <font color='blue'>iFlyChatConfig</font>) value is set to "YES", then it automatically retrieves a new session key from the server and connects the chat. 

    After the chat is connected to the server, iFlyChatLibrary will throw a NSNotification with a dictionary of user's details as <font color='blue'>iFlyChatUser</font> object with key <font color='blue'>"iFlyChatCurrentUser"</font> and session key used to connect to the chat. with key <font color='blue'>"sessionKey"</font>. The notification name would be <font color='blue'>"iFlyChat.onChatConnect"</font>. 


8. To listen to <font color='blue'>"iFlyChat.onChatConnect"</font> event, the user needs to add the observer for this notification and retrieve the <font color='blue'>iFlyChatUser</font> object and session key string from the notification object.

    <code>
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onChatConnect:) name:@”iFlyChat.onChatConnect” object:nil];  

    -(void) onChatConnect:(NSNotification *)notification  
    {  
        id object = [notification object];  
        iFlyChatUser *currentUser = [object objectForKey:@"iFlyChatCurrentUser"];  
        NSString *sessionKey = [object objectForKey:@"sessionKey"];  
    }  


    SWIFT  

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
    </code>

##Disconnection

1. To disconnect the chat, the user needs to call the following function of the <font color='blue'>iFlyChatService</font> object

    <code>
    OBJECTIVE-C

    [service disconnectChat];


    SWIFT

    service.disconnectChat()
    </code>
  
    Along with calling this function, the user needs to remove the NSNotification observers for clean disconnection.

    The disconnection method must also be called when the app terminates, i.e., in the app delegate. This will ensure clean closure of the connection of the client to the server and iFlyChatLibrary to the UI of the application.


    After the chat is disconnected from the server, iFlyChatLibrary will throw a NSNotification name <font color='blue'>"iFlyChat.onChatDisconnect"</font> to allow the users to perform final clean up. 

    To listen to <font color='blue'>"iFlyChat.onChatDisconnect"</font> event, the user needs to add the observer for this notification.

    <code>
    OBJECTIVE-C  

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onChatDisconnect:) name:@”iFlyChat.onChatDisconnect” object:nil];  

    -(void) onChatDisconnect:(NSNotification *)notification  
    {  
        //perform  your clean up   
    }  


    SWIFT  

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
    </code>

#Sending and receiving messages


1. Send message/file to user

    To send a message to user, the first person needs to create an object of <font color='blue'>iFlyChatMessage</font> object with the required parameters and pass that object to the <font color='blue'>iFlyChatService</font> object's method <font color='blue'>"sendMessagetoUser"</font>:

    <code>
    OBJECTIVE-C

    iFlyChatMessage *msg = [[iFlyChatMessage alloc] initIFlyChatMessageObjectwithMessage:@"Message for User" fromName:@”John” toName:@"Prateek" fromId:@"1" toId:@"2" message_id:@"" color:@"" fromProfileUrl:@"" fromAvatarUrl:@"" fromRole:@"" time:@"", type:@"user"];​

    [service sendMessagetoUser:msg];

    SWIFT

    var msg: iFlyChatMessage = iFlyChatMessage(IFlyChatMessageObjectwithMessage: "Message for user", fromName: "John", toName: "Prateek", fromId: "1", toId: "2", message_id: "", color: "", fromProfileUrl: "", fromAvatarUrl: "", fromRole: "", time: "", type: "user")

    service.sendMessagetoUser(msg)
    </code>
  
    <font color='blue'>Message text</font>, <font color='blue'>fromName</font>, <font color='blue'>toName</font>, <font color='blue'>fromId</font> and <font color='blue'>toId</font> are the required parameters to create this message object otherwise the class will throw an exception. In case of sending file, the user needs to send the asset or file URL of the file as string in message text.

    The user should leave the <font color='blue'>message_id</font> and <font color='blue'>time</font> fields as empty strings because the iFlyChatLibrary itself creates those parameters and insert them into the final message that is sent to the server.

    <font color='blue'>color</font>, <font color='blue'>fromProfileUrl</font>, <font color='blue'>fromAvatarUrl</font> and <font color='blue'>fromRole</font> are some of the optional parameters and can be left empty if not available.

    <font color='blue'>type</font> specifies whether the message object being created is for room or user.


2. Send message/file to room

    To send a message to room, the first person needs to create an object of <font color='blue'>iFlyChatMessage</font> object with the required parameters and pass that object to the <font color='blue'>iFlyChatService</font> object's method <font color='blue'>"sendMessagetoRoom"</font>:

    <code>
    OBJECTIVE-C

    iFlyChatMessage *msg = [[iFlyChatMessage alloc] initIFlyChatMessageObjectwithMessage:@"Message for Room" fromName:@”John” toName:@"Public Chatroom" fromId:@"1" toId:@"0" message_id:@"" color:@"" fromProfileUrl:@"" fromAvatarUrl:@"" fromRole:@"" time:@"", type:@"room"];​

    [service sendMessagetoRoom:msg];

    SWIFT

    let msg: iFlyChatMessage = iFlyChatMessage(IFlyChatMessageObjectwithMessage: "Message for Room", fromName: "John", toName: "Public Chatroom", fromId: "1", toId: "0", message_id: "", color: "", fromProfileUrl: "", fromAvatarUrl: "", fromRole: "", time: "", type:"room")

    service.sendMessagetoRoom(msg)
    </code>
  
    <font color='blue'>Message text</font>, <font color='blue'>fromName</font>, <font color='blue'>toName</font>, <font color='blue'>fromId</font> and <font color='blue'>toId</font> are the required parameters to create this message object otherwise the class will throw an exception. In case of sending file, the user needs to send the asset or file URL of the file as string in message text.

    The user should leave the <font color='blue'>message_id</font> and <font color='blue'>time</font> fields as empty strings because the iFlyChatLibrary itself creates those parameters and insert them into the final message that is sent to the server.

    <font color='blue'>color</font>, <font color='blue'>fromProfileUrl</font>, <font color='blue'>fromAvatarUrl</font> and <font color='blue'>fromRole</font> are some of the optional parameters and can be left empty if not available.

    <font color='blue'>type</font> specifies whether the message object being created is for room or user.


3. Receiving message/file from user

    When some other user sends a message to the first user, iFlyChatLibrary throws a NSNotification with the <font color='blue'>iFlyChatMessage</font> object and name <font color='blue'>"iFlyChat.onMessagefromUser"</font>. Therefore, it is required that the application must listen to this notification in order to receive the message from the user and then the user can process the message. In case of receiving a file, the message field will contain the URL of the file from where it can be downloaded.

    To listen to this notification and receive the message, the user needs to add observer to the application and retrieve the <font color='blue'>iFlyChatMessage</font> object from the notification:

    <code>
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(receiveMessage:) name:@”iFlyChat.onMessagefromUser” object:nil];

    -(void) receiveMessage:(NSNotification *)notification
    {
        iFlyChatMessage *msg = [notification object];
    }


    SWIFT

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
    </code>
  
4. Receiving message from room

    When some other room sends a message to the user, iFlyChatLibrary throws a NSNotification with the <font color='blue'>iFlyChatMessage</font> object and name <font color='blue'>"iFlyChat.onMessagefromRoom"</font>. Therefore, it is required that the application must listen to this notification in order to receive the message from the room and then the user can process the message. In case of receiving a file, the message field will contain the URL of the file from where it can be downloaded.

    To listen to this notification and receive the message, the user needs to add observer to the application and retrieve the <font color='blue'>iFlyChatMessage</font> object from the notification:

    <code>
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(receiveMessage:) name:@”iFlyChat.onMessagefromRoom” object:nil];

    -(void) receiveMessage:(NSNotification *)notification
    {
        iFlyChatMessage *msg = [notification object];
    }


    SWIFT

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
    </code>
  
5. Receiving Global List

    iFlyChatLibrary polls every 2 min to the server to get the updated user and room list, together which we call as Global list or Roster. Whenever the iFlyChatLibrary gets the global list from the server, it throws a NSNotification with <font color='blue'>iFlyChatRoster</font> object and name <font color='blue'>"iFlyChat.onGlobalListUpdate"</font>. Therefore, it is required that the application must listen to this notification in order to receive the updated global list form the server and render it in the view.

    To listen to this notification and receive the updated global list, the user needs to add observer to the application and retrieve the <font color='blue'>iFlyChatRoster</font> object from the notification:

    <code>
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(receiveGlobalList:) name:@”iFlyChat.onGlobalListUpdate” object:nil];

    -(void) receiveGlobalList:(NSNotification *)notification
    {
        iFlyChatRoster *updatedRoster = [notification object];
        //Now here, you can get userList and roomList separately by calling
        iFlyChatOrderedDictionary *userList = [updatedRoster getUserList];
        iFlyChatOrderedDictionary *roomList = [updatedRoster getRoomLIst];
    }


    SWIFT

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
    </code>
  
    Here, the <font color='blue'>iFlyChatRoster</font> object actually returns two <font color='blue'>iFlyChatOrderedDictionary</font> objects, one for <font color='blue'>Userlist</font> and the other for <font color='blue'>Roomlist</font>. These data structure types can be retrieved from the iFlyChatRoster object using the getter functions provided in the same. 

    To render userlist and roomlist in a tableview, it is required that the data source be an array. Therefore, we have made this custom data structure that provides the functionality of a dictionary and an array together.