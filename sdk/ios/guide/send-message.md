#Sending and receiving messages


1. Send message to user

    To send a message to user, the first person needs to create an object of `iFlyChatMessage` object with the required parameters and pass that object to the `iFlyChatService` object's method `"sendMessagetoUser"`:

    ```obj-c
    //OBJECTIVE-C

    iFlyChatMessage *msg = [[iFlyChatMessage alloc] initIFlyChatMessageObjectwithMessage:@"Message for User" fromName:@”John” toName:@"Prateek" fromId:@"1" toId:@"2" message_id:@"" color:@"" fromProfileUrl:@"" fromAvatarUrl:@"" fromRole:@"" time:@"", type:@"user"];​

    [service sendMessagetoUser:msg];
    ```
    ```swift
    //SWIFT

    var msg: iFlyChatMessage = iFlyChatMessage(IFlyChatMessageObjectwithMessage: "Message for user", fromName: "John", toName: "Prateek", fromId: "1", toId: "2", message_id: "", color: "", fromProfileUrl: "", fromAvatarUrl: "", fromRole: "", time: "", type: "user")

    service.sendMessagetoUser(msg)
    ```
  
    >`Message text`, `fromName`, `toName`, `fromId` and `toId` are the required parameters to create this message object otherwise the class will throw an exception.

    >The user should leave the `message_id` and `time` fields as empty strings because the iFlyChatLibrary itself creates those parameters and insert them into the final message that is sent to the server.

    >`color`, `fromProfileUrl`, `fromAvatarUrl` and `fromRole` are some of the optional parameters and can be left empty if not available.

    >`type` specifies whether the message object being created is for room or user.


2. Send message to room

    To send a message to room, the first person needs to create an object of `iFlyChatMessage` object with the required parameters and pass that object to the `iFlyChatService` object's method `"sendMessagetoRoom"`:

    ```obj-c
    //OBJECTIVE-C

    iFlyChatMessage *msg = [[iFlyChatMessage alloc] initIFlyChatMessageObjectwithMessage:@"Message for Room" fromName:@”John” toName:@"Public Chatroom" fromId:@"1" toId:@"0" message_id:@"" color:@"" fromProfileUrl:@"" fromAvatarUrl:@"" fromRole:@"" time:@"", type:@"room"];​

    [service sendMessagetoRoom:msg];
    ```
    ```swift
    //SWIFT

    let msg: iFlyChatMessage = iFlyChatMessage(IFlyChatMessageObjectwithMessage: "Message for Room", fromName: "John", toName: "Public Chatroom", fromId: "1", toId: "0", message_id: "", color: "", fromProfileUrl: "", fromAvatarUrl: "", fromRole: "", time: "", type:"room")

    service.sendMessagetoRoom(msg)
    ```
  
    >`Message text`, `fromName`, `toName`, `fromId` and `toId` are the required parameters to create this message object otherwise the class will throw an exception.

    >The user should leave the `message_id` and `time` fields as empty strings because the iFlyChatLibrary itself creates those parameters and insert them into the final message that is sent to the server.

    >`color`, `fromProfileUrl`, `fromAvatarUrl` and `fromRole` are some of the optional parameters and can be left empty if not available.

    >`type` specifies whether the message object being created is for room or user.


3. Receiving message from user

    When some other user sends a message to the first user, iFlyChatLibrary throws a NSNotification with the `iFlyChatMessage` object and name `"iFlyChat.onMessagefromUser"`. Therefore, it is required that the application must listen to this notification in order to receive the message from the user and then the user can process the message.

    To listen to this notification and receive the message, the user needs to add observer to the application and retrieve the `iFlyChatMessage` object from the notification:

    ```obj-c
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(receiveMessage:) name:@”iFlyChat.onMessagefromUser” object:nil];

    -(void) receiveMessage:(NSNotification *)notification
    {
        iFlyChatMessage *msg = [notification object];
    }
    ```
    ```swift
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
    ```
  
4. Receiving message from room

    When some other room sends a message to the user, iFlyChatLibrary throws a NSNotification with the `iFlyChatMessage` object and name `"iFlyChat.onMessagefromRoom"`. Therefore, it is required that the application must listen to this notification in order to receive the message from the room and then the user can process the message.

    To listen to this notification and receive the message, the user needs to add observer to the application and retrieve the `iFlyChatMessage` object from the notification:

    ```obj-c
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(receiveMessage:) name:@”iFlyChat.onMessagefromRoom” object:nil];

    -(void) receiveMessage:(NSNotification *)notification
    {
        iFlyChatMessage *msg = [notification object];
    }
    ```
    ```swift
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
    ```