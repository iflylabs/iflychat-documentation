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

    To delete a message from private chat, the user needs to call a function from the <font color='blue'>iFlyChatService</font> object and pass the message id of the message and user id from whose private chat the message is to be deleted as the parameter.

    <code>
    OBJECTIVE-C

    [service deleteChatMessageFromUser:@"m_12345678_01234567_123456789" userId:@"12345678"];

    SWIFT

    service.deleteChatMessageFromUser("m_12345678_01234567_123456789","12345678")
    </code>
  
    If the other user has deleted the message from the private chat between you and that user, you will get a notification about this event. iFlyChatLibrary throws a NSNotification with <font color='blue'>message id</font> of the message that was deleted and name <font color='blue'>"iFlyChat.onDeleteChatMessageFromUser"</font> so that each client can update its view right away.

    To listen to this notification and receive the delete message event, the user needs to add observer to the application and retrieve the message id string from the notification:

    <code>
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onDeleteMessageFromUser:) name:@”iFlyChat.onDeleteMessageFromUser” object:nil];

    -(void) onDeleteMessageFromUser:(NSNotification *)notification
    {
        NSString *messageid = [notification object];
    }


    SWIFT

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
    </code>
  
2. Delete a message from public chatroom

    To delete a message from public chatroom, the user needs to call a function from the <font color='blue'>iFlyChatService</font> object and pass the <font color='blue'>message id</font> of the message and room id from where the message is to be deleted as the parameter.

    <code>
    OBJECTIVE-C

    [service deleteChatMessageFromRoom:@"m_12345678_0_123456789" roomId:@"0"];

    SWIFT

    service.deleteChatMessageFromUser("m_12345678_0_123456789","0")
    </code>
  
    If the other user has deleted the message from the public chatroom, every user in that chatroom will get a notification about this event. iFlyChatLibrary throws a NSNotification with message id of the message that was deleted and name <font color='blue'>"iFlyChat.onDeleteChatMessageFromRoom"</font> so that each client can update its view right away.

    To listen to this notification and receive the delete message event, the user needs to add observer to the application and retrieve the message id string from the notification:

    <code>
    OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onDeleteMessageFromRoom:) name:@”iFlyChat.onDeleteMessageFromRoom” object:nil];

    -(void) onDeleteMessageFromRoom:(NSNotification *)notification
    {
        NSString *messageid = [notification object];
    }


    SWIFT

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
    </code>