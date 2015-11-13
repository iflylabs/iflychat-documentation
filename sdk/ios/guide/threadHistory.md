#Getting Message History  

Users can also get message history from iFlyChat servers for both rooms and users.

1. Get message history for users

    To get message history for a user, one needs to call a function from the iFlyChatService object and pass the various required parameters.

    <code>
    OBJECTIVE-C

    [service getUserThreadHistoryWithCurrentUserId:<logged in user id> forUserId:<user id of the user> forUserName:<user name of the user> messageId:<message id of the oldest available message>];

    SWIFT

    service.getUserThreadHistoryWithCurrentUserId(<logged in user id>,forUserId:<user id of the user>,forUserName:<user name of the user>,messageId:<message id of the oldest available message>)
    </code>  


    After calling these functions, iFlyChat servers will send the thread history for the user. After processing the message, iFlyChatLibrary will send a notification named <font color='blue'>"iFlyChat.onUserThreadHistory"</font> if the thread history is available otherwise <font color='blue'>"iFlyChat.onEmptyThreadHistory"</font> if the thread history is empty.


    To listen to this notification and receive the <font color='blue'>onThreadHistory</font> event, the user needs to add observer to the application and retrieve the <font color='blue'>"forUserId"</font> string and <font color='blue'>iFlyChatOrderedDictionary</font> object from the notification:

    <code>
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onUserThreadHistory:) name:@”iFlyChat.onUserThreadHistory” object:nil];

    -(void) onUserThreadHistory:(NSNotification *)notification
    {
        NSDictionary *result = [notification object];
        if([[result objectForKey:@"forUserId"] isEqualToString:<current user id>])
        {
            iFlyChatOrderedDictionary *threadHistory = [result objectForKey:@"threadHistory"];
        }
    }


    SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "onUserThreadHistory:",
        name: "iFlyChat.onUserThreadHistory",
        object: nil
    )

    func onUserThreadHistory(notification: NSNotification)
    {
        let result:NSDictionary = notification.object as! NSDictionary
        if result.objectForKey("forUserId").isEqualToString("<current user id>")
        {
            let threadHistory:iFlyChatOrderedDictionary = notification.object! as! iFlyChatOrderedDictionary
        }
    }
    </code>  

    NOTE: If the thread history is empty, iFlyChatLibrary will send a notification with only one object, i.e., a <font color='blue'>"forId"</font> string which can be empty also.  


2. Get message history for room

    To get message history for a room, one needs to call a function from the <font color='blue'>iFlyChatService</font> object and pass the various required parameters.

    <code>
    OBJECTIVE-C

    [service getRoomThreadHistoryWithCurrentUserId:<logged in user id> forUserId:<room id of the room> forRoomName:<room name of the room> messageId:<message id of the oldest available message>];

    SWIFT

    service.getRoomThreadHistoryWithCurrentUserId(<logged in user id>,forUserId:<room id of the room>,forRoomName:<room name of the room>,messageId:<message id of the oldest available message>)
    </code>  

    After calling these functions, iFlyChat servers will send the thread history for the room. After processing the message, iFlyChatLibrary will send a notification named <font color='blue'>"iFlyChat.onRoomThreadHistory"</font> if the thread history is available otherwise <font color='blue'>"iFlyChat.onEmptyThreadHistory"</font> if the thread history is empty.


    To listen to this notification and receive the <font color='blue'>onThreadHistory</font> event, the user needs to add observer to the application and retrieve the <font color='blue'>"forRoomId"</font> string and <font color='blue'>iFlyChatOrderedDictionary</font> object from the notification:

    <code>
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onRoomThreadHistory:) name:@”iFlyChat.onRoomThreadHistory” object:nil];

    -(void) onRoomThreadHistory:(NSNotification *)notification
    {
        NSDictionary *result = [notification object];
        if([[result objectForKey:@"forRoomId"] isEqualToString:<current room id>])
        {
            iFlyChatOrderedDictionary *threadHistory = [result objectForKey:@"threadHistory"];
        }
    }


    SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "onRoomThreadHistory:",
        name: "iFlyChat.onRoomThreadHistory",
        object: nil
    )

    func onRoomThreadHistory(notification: NSNotification)
    {
        let result:NSDictionary = notification.object as! NSDictionary
        if result.objectForKey("forRoomId").isEqualToString("<current room id>")
        {
            let threadHistory:iFlyChatOrderedDictionary = notification.object! as! iFlyChatOrderedDictionary
        }
    }
    </code>  

    NOTE: If the thread history is empty, iFlyChatLibrary will send a notification with only one object, i.e., a <font color='blue'>"forId"</font> string which can be empty also.