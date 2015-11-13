#Message History Moderation

Users with sufficient privileges can clear the entire message history from private and public chats.

Following is a table that details out the which operation requires admin level privileges:
    
| Operation                                     | Admin? |
|-----------------------------------------------|--------|
| Clear message history from other private chat | No     |
| Clear message history from other public chat  | Yes    |


1. Clear message history from private chat

    To clear the message history from private chat, the user needs to call a function from the <font color='blue'>iFlyChatService</font> object and pass the user id from whose private chat the message history is to be cleared, as the parameter.

    <code>
    OBJECTIVE-C

    [service clearUserThreadHistory:@"12345678"];

    SWIFT

    service.clearUserThreadHistory("12345678")
    </code>

    If the other user has cleared the message history from the private chat between you and that user, you will get a notification about this event. iFlyChatLibrary throws a NSNotification with user id of the user from whose private chat the message history was cleared and name <font color='blue'>"iFlyChat.onUserThreadHistoryClear"</font> so that each client can update its view right away.

    To listen to this notification and receive the clear message history event, the user needs to add observer to the application and retrieve the user id string from the notification:

    <code>
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onUserThreadHistoryClear:) name:@”iFlyChat.onUserThreadHistoryClear” object:nil];

    -(void) onUserThreadHistoryClear:(NSNotification *)notification
    {
        NSString *userid = [notification object];
    }


    SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "onUserThreadHistoryClear:",
        name: "iFlyChat.onUserThreadHistoryClear",
        object: nil
    )

    func onUserThreadHistoryClear(notification: NSNotification)
    {
        let userid: String = notification.object! as! String
    }
    </code>

2. Clear the message history from public chatroom

    To clear the message history from public chatroom, the user needs to call a function from the <font color='blue'>iFlyChatService</font> object and pass the room id from where the message history is to be cleared, as the parameter.

    <code>
    OBJECTIVE-C

    [service onRoomThreadHistoryClear:@"0"];

    SWIFT

    service.onRoomThreadHistoryClear("0")
    </code>

    If the other user has cleared the message history from the public chatroom, every user in that chatroom will get a notification about this event. iFlyChatLibrary throws a NSNotification with room id of the room from where the message history was cleared and name <font color='blue'>"iFlyChat.onRoomThreadHistoryClear"</font> so that each client can update its view right away.

    To listen to this notification and receive the clear message history event, the user needs to add observer to the application and retrieve the room id string from the notification:

    <code>
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onRoomThreadHistoryClear:) name:@”iFlyChat.onRoomThreadHistoryClear” object:nil];

   -(void) onRoomThreadHistoryClear:(NSNotification *)notification
    {
        NSString *roomid = [notification object];
    }


    SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "onRoomThreadHistoryClear:",
        name: "iFlyChat.onRoomThreadHistoryClear",
        object: nil
    )

    func onRoomThreadHistoryClear(notification: NSNotification)
    {
        let roomid: String = notification.object! as! String
    }
    </code>