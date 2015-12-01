#User Moderation

Apart from messaging, the user can also perform some admin level operations and receive some admin level operations' events performed by other users. These operations are as follows:

1. Kick a user

    To kick a user, the first requirement is that the first user must be an admin. If the first user is admin, all he needs to do is call a function of `iFlyChatService` object and pass the user id of the user who needs to be kicked:

    ~~~
    //OBJECTIVE-C

    [service kickUser:@"12345678"];
    ~~~

    ~~~
    //SWIFT

    service.kickUser("12345678")
    ~~~
  
    If some other admin has kicked some other user, everybody connected on the chat gets a notification about this event. iFlyChatLibrary throws a NSNotification with user id of the user kicked and name `"iFlyChat.onUserKick"` so that each client can update its view right away (although the updated global list will exclude that user given that the kicked user has not reconnected to the chat again).

    To listen to this notification and receive the kick user event, the user needs to add observer to the application and retrieve the user id string from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(userKick:) name:@”iFlyChat.onUserKick” object:nil];

    -(void) userKick:(NSNotification *)notification
    {
        NSString *userid = [notification object];
    }
    ~~~

    ~~~
    //SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "userKick:",
        name: "iFlyChat.onUserKick",
        object: nil
    )

    func userKick(notification: NSNotification)
    {
        let userid: String = notification.object! as! String
    }
    ~~~
  
2. Ban a user

    To ban a user, the first requirement is that the first user must be an admin. If the first user is admin, all he needs to do is call a function of `iFlyChatService` object and pass the user id of the user who needs to be banned:

    ~~~
    //OBJECTIVE-C

    [service banUser:@"12345678"];
    ~~~

    ~~~
    //SWIFT

    service.banUser("12345678")
    ~~~
  
    If some other admin has banned some other user, everybody connected on the chat gets a notification about this event. iFlyChatLibrary throws a NSNotification with user id of the user banned and name `"iFlyChat.onUserBan"` so that each client can update its view right away (although the updated global list will exclude that user given that the banned user is not unbanned by the admin).

    To listen to this notification and receive the ban user event, the user needs to add observer to the application and retrieve the user id string from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(userBan:) name:@”iFlyChat.onUserBan” object:nil];

    -(void) userBan:(NSNotification *)notification
    {
        NSString *userid = [notification object];
    }
    ~~~

    ~~~
    //SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "userBan:",
        name: "iFlyChat.onUserBan",
        object: nil
    )

    func userBan(notification: NSNotification)
    {
        let userid: String = notification.object! as! String
    }
    ~~~
  
3. Ban the IP of a user

    To ban the IP of a user, the first requirement is that the first user must be an admin. If the first user is admin, all he needs to do is call a function of `iFlyChatService` object and pass the user id of the user whose IP needs to be banned:

    ~~~
    //OBJECTIVE-C

    [service banIp:@"12345678"];
    ~~~

    ~~~
    //SWIFT

    service.banIp("12345678")
    ~~~
  
    If some other admin has banned the IP of some other user, everybody connected on the chat gets a notification about this event. iFlyChatLibrary throws a NSNotification with user id of the user whose IP was banned and name `"iFlyChat.onUserBanIp"` so that each client can update its view right away (although the updated global list will exclude that user given that the banned IP is not unbanned by the admin).

    To listen to this notification and receive the ban ip user event, the user needs to add observer to the application and retrieve the user id string from the notification:

    ~~~
    //OBJECTIVE-C

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(userBanIp:) name:@”iFlyChat.onUserBanIp” object:nil];

    -(void) userBanIp:(NSNotification *)notification
    {
        NSString *userid = [notification object];
    }
    ~~~
    
    ~~~
    //SWIFT

    NSNotificationCenter.defaultCenter().addObserver
    (
        self,
        selector: "userBanIp:",
        name: "iFlyChat.onUserBanIp",
        object: nil
    )

    func userBanIp(notification: NSNotification)
    {
        let userid: String = notification.object! as! String
    }
    ~~~