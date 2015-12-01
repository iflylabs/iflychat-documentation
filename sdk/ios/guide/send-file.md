#Sending and receiving files


1. Send file to user

    To send a file to user, the first person needs to create an object of `iFlyChatMessage` object with the required parameters where the message should contain the asset or file URL of the file in string format and pass that object to the `iFlyChatService` object's method `"sendFiletoUser"`:

    ~~~
    //OBJECTIVE-C

    iFlyChatMessage *msg = [[iFlyChatMessage alloc] initIFlyChatMessageObjectwithMessage:@"<Asset or File URL>" fromName:@”John” toName:@"Prateek" fromId:@"1" toId:@"2" message_id:@"" color:@"" fromProfileUrl:@"" fromAvatarUrl:@"" fromRole:@"" time:@"", type:@"user"];​

    [service sendFiletoUser:msg];
    ~~~

    ~~~
    //SWIFT

    var msg: iFlyChatMessage = iFlyChatMessage(IFlyChatMessageObjectwithMessage: "<Asset or File URL>", fromName: "John", toName: "Prateek", fromId: "1", toId: "2", message_id: "", color: "", fromProfileUrl: "", fromAvatarUrl: "", fromRole: "", time: "", type: "user")

    service.sendFiletoUser(msg)
    ~~~
  
    >`Message text`, `fromName`, `toName`, `fromId` and `toId` are the required parameters to create this message object otherwise the class will throw an exception. Here message text contains the asset or file URL in string format.

    >The user should leave the `message_id` and `time` fields as empty strings because the iFlyChatLibrary itself creates those parameters and insert them into the final message that is sent to the server.

    >`color`, `fromProfileUrl`, `fromAvatarUrl` and `fromRole` are some of the optional parameters and can be left empty if not available.

    >`type` specifies whether the message object being created is for room or user.


2. Send message to room

    To send a file to room, the first person needs to create an object of `iFlyChatMessage` object with the required parameters where the message should contain the asset or file URL of the file in string format and pass that object to the `iFlyChatService` object's method `"sendFiletoRoom"`:

    ~~~
    //OBJECTIVE-C

    iFlyChatMessage *msg = [[iFlyChatMessage alloc] initIFlyChatMessageObjectwithMessage:@"<Asset or File URL>" fromName:@”John” toName:@"Public Chatroom" fromId:@"1" toId:@"0" message_id:@"" color:@"" fromProfileUrl:@"" fromAvatarUrl:@"" fromRole:@"" time:@"", type:@"room"];​

    [service sendFiletoRoom:msg];
    ~~~

    ~~~
    //SWIFT

    let msg: iFlyChatMessage = iFlyChatMessage(IFlyChatMessageObjectwithMessage: "<Asset or File URL>", fromName: "John", toName: "Public Chatroom", fromId: "1", toId: "0", message_id: "", color: "", fromProfileUrl: "", fromAvatarUrl: "", fromRole: "", time: "", type:"room")

    service.sendFiletoRoom(msg)
    ~~~
  
    >`Message text`, `fromName`, `toName`, `fromId` and `toId` are the required parameters to create this message object otherwise the class will throw an exception. Here message text contains the asset or file URL in string format.

    >The user should leave the `message_id` and `time` fields as empty strings because the iFlyChatLibrary itself creates those parameters and insert them into the final message that is sent to the server.

    >`color`, `fromProfileUrl`, `fromAvatarUrl` and `fromRole` are some of the optional parameters and can be left empty if not available.

    >`type` specifies whether the message object being created is for room or user.


3. Receiving file from user

    When some other user sends a file to the first user, iFlyChatLibrary throws a NSNotification with the `iFlyChatMessage` object with the link for the file as message text and name `"iFlyChat.onMessagefromUser"`. Therefore, it is required that the application must listen to this notification in order to receive the file from the user and then the user can process the message.

    To listen to this notification and receive the file, the user needs to add observer to the application and retrieve the `iFlyChatMessage` object from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(receiveMessage:) name:@”iFlyChat.onMessagefromUser” object:nil];

    -(void) receiveMessage:(NSNotification *)notification
    {
        iFlyChatMessage *msg = [notification object];
        NSString *fileURL = msg.getMessage;
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
        let fileURL:NSString = msg.getMessage() as! NSString
    }
    ~~~
  
4. Receiving file from room

    When some other room sends a file to the user, iFlyChatLibrary throws a NSNotification with the `iFlyChatMessage` object with the link for the file as message text and name `"iFlyChat.onMessagefromRoom"`. Therefore, it is required that the application must listen to this notification in order to receive the file from the room and then the user can process the message.

    To listen to this notification and receive the file, the user needs to add observer to the application and retrieve the `iFlyChatMessage` object from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(receiveMessage:) name:@”iFlyChat.onMessagefromRoom” object:nil];

    -(void) receiveMessage:(NSNotification *)notification
    {
        iFlyChatMessage *msg = [notification object];
        NSString *fileURL = msg.getMessage;
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
        let fileURL:NSString = msg.getMessage() as! NSString
    }
    ~~~