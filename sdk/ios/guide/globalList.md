#Receiving Global List

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