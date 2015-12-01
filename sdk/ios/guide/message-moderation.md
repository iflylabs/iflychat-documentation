#Message Moderation

Users with sufficient privileges can delete messages from private and public chats.

Following is a table that details out the which operation requires admin level privileges:

| Operation                                      | Admin? |
|------------------------------------------------|--------|
| Delete other user messages from private chat   | Yes    |
| Delete our own message from private chat       | No     |
| Delete other user message from public chatroom | Yes    |
| Delete our own message from public chatroom    | Yes    |


1. Delete a message from private chat

    To delete a message from private chat, the user needs to call a function from the `iFlyChatService` object and pass the message id of the message and user id from whose private chat the message is to be deleted as the parameter.

    ~~~
    //OBJECTIVE-C

    [service deleteChatMessageFromUser:@"m_12345678_01234567_123456789" userId:@"12345678"];
    ~~~
    ~~~
    //SWIFT

    service.deleteChatMessageFromUser("m_12345678_01234567_123456789","12345678")
    ~~~
  
    If the other user has deleted the message from the private chat between you and that user, you will get a notification about this event. iFlyChatLibrary throws a NSNotification with `message id` of the message that was deleted and name `"iFlyChat.onDeleteChatMessageFromUser"` so that each client can update its view right away.

    To listen to this notification and receive the delete message event, the user needs to add observer to the application and retrieve the message id string from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onDeleteMessageFromUser:) name:@”iFlyChat.onDeleteMessageFromUser” object:nil];

    -(void) onDeleteMessageFromUser:(NSNotification *)notification
    {
        NSString *messageid = [notification object];
    }
    ~~~
    ~~~
    //SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "onDeleteMessageFromUser:",
        name: "iFlyChat.onDeleteMessageFromUser",
        object: nil
    )

    func onDeleteMessageFromUser(notification: NSNotification)
    {
        let messageid: String = notification.object! as! String
    }
    ~~~
  
2. Delete a message from public chatroom

    To delete a message from public chatroom, the user needs to call a function from the `iFlyChatService` object and pass the `message id` of the message and room id from where the message is to be deleted as the parameter.

    ~~~
    //OBJECTIVE-C

    [service deleteChatMessageFromRoom:@"m_12345678_0_123456789" roomId:@"0"];
    ~~~
    ~~~
    //SWIFT

    service.deleteChatMessageFromUser("m_12345678_0_123456789","0")
    ~~~
  
    If the other user has deleted the message from the public chatroom, every user in that chatroom will get a notification about this event. iFlyChatLibrary throws a NSNotification with message id of the message that was deleted and name `"iFlyChat.onDeleteChatMessageFromRoom"` so that each client can update its view right away.

    To listen to this notification and receive the delete message event, the user needs to add observer to the application and retrieve the message id string from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onDeleteMessageFromRoom:) name:@”iFlyChat.onDeleteMessageFromRoom” object:nil];

    -(void) onDeleteMessageFromRoom:(NSNotification *)notification
    {
        NSString *messageid = [notification object];
    }
    ~~~
    ~~~
    //SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "onDeleteMessageFromRoom:",
        name: "iFlyChat.onDeleteMessageFromRoom",
        object: nil
    )

    func onDeleteMessageFromUser(notification: NSNotification)
    {
        let messageid: String = notification.object! as! String
    }
    ~~~

#Message History Moderation

Users with sufficient privileges can clear the entire message history from private and public chats.

Following is a table that details out the which operation requires admin level privileges:
    
| Operation                                     | Admin? |
|-----------------------------------------------|--------|
| Clear message history from other private chat | No     |
| Clear message history from other public chat  | Yes    |


1. Clear message history from private chat

    To clear the message history from private chat, the user needs to call a function from the `iFlyChatService` object and pass the user id from whose private chat the message history is to be cleared, as the parameter.

    ~~~
    //OBJECTIVE-C

    [service clearUserThreadHistory:@"12345678"];
    ~~~
    ~~~
    //SWIFT

    service.clearUserThreadHistory("12345678")
    ~~~

    If the other user has cleared the message history from the private chat between you and that user, you will get a notification about this event. iFlyChatLibrary throws a NSNotification with user id of the user from whose private chat the message history was cleared and name `"iFlyChat.onUserThreadHistoryClear"` so that each client can update its view right away.

    To listen to this notification and receive the clear message history event, the user needs to add observer to the application and retrieve the user id string from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onUserThreadHistoryClear:) name:@”iFlyChat.onUserThreadHistoryClear” object:nil];

    -(void) onUserThreadHistoryClear:(NSNotification *)notification
    {
        NSString *userid = [notification object];
    }
    ~~~
    ~~~
    //SWIFT

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
    ~~~

2. Clear the message history from public chatroom

    To clear the message history from public chatroom, the user needs to call a function from the `iFlyChatService` object and pass the room id from where the message history is to be cleared, as the parameter.

    ~~~
    //OBJECTIVE-C

    [service onRoomThreadHistoryClear:@"0"];
    ~~~
    ~~~
    //SWIFT

    service.onRoomThreadHistoryClear("0")
    ~~~

    If the other user has cleared the message history from the public chatroom, every user in that chatroom will get a notification about this event. iFlyChatLibrary throws a NSNotification with room id of the room from where the message history was cleared and name `"iFlyChat.onRoomThreadHistoryClear"` so that each client can update its view right away.

    To listen to this notification and receive the clear message history event, the user needs to add observer to the application and retrieve the room id string from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onRoomThreadHistoryClear:) name:@”iFlyChat.onRoomThreadHistoryClear” object:nil];

    -(void) onRoomThreadHistoryClear:(NSNotification *)notification
    {
        NSString *roomid = [notification object];
    }
    ~~~
    ~~~
    //SWIFT

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
    ~~~