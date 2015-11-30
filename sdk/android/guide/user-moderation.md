###User Moderation

Apart from messaging, the user can also perform some admin level operations and receive some admin level operations' events performed by other users. These operations are as follows:

* Kick a user
* Ban a user
* Ban the IP of a user

<br>
**Kick a user**

To kick a user, the first requirement is that the first user must be an admin. If the first user is admin, all he needs to do is call a function of `iFlyChatService` object and pass the user id string of the user who needs to be kicked:
```
service.kickUser(userId);
```
<br>
If some other admin has kicked some other user, everybody connected to the chat gets a broadcast about this event. iFlyChatLibrary sends a broadcast with user id of the user kicked, this broadcast intent have intent action named `iFlyChat.onUserKick` so that each client can update its view right away (although the updated global list will exclude that user given that the kicked user has not reconnected to the chat again).

To listen to this broadcast and receive the event `iFlyChat.onUserKick`. The user needs to match the intent action in the application's `onReceive()` method. To retrieve the user id string. Firstly, user needs to create and initialize the Bundle type object `bundleData`. Then user can get `userId` string by calling `getString("userId")` method on data a Bundle type object :


```
if(intent.getAction().equals("iFlyChat.onUserKick")){
    Bundle bundleData = intent.getExtras();
    String userId = bundleData.getString("userId");
}
```
<br>

**Ban a user**

To ban a user, the first requirement is that the first user must be an admin. If the first user is admin, all he needs to do is call a function of `iFlyChatService` object and pass the user id of the user who needs to be banned:
```
service.banUser(userId);
```
<br>
If some other admin has banned some other user, everybody connected to the chat gets a broadcast about this event. iFlyChatLibrary sends a broadcast with user id of the user banned, this broadcast intent have intent action named `iFlyChat.onUserBan` so that each client can update its view right away (although the updated global list will exclude that user given that the banned user is not unbanned by the admin).

To listen to this broadcast and receive the event `iFlyChat.onUserBan`. The user needs to match the intent action in the application's onReceive() method. To retrieve the user id string. Firstly, user needs to create and initialize the Bundle type object `bundleData`. Then user can get `userId` string by calling `getString("userId")` method on data a Bundle type object :
```
if(intent.getAction().equals("iFlyChat.onUserBan")){
    Bundle bundleData = intent.getExtras();
    String userId = bundleData.getString("userId");
}
```
<br>

**Ban the IP of a user**

To ban the IP of a user, the first requirement is that the first user must be an admin. If the first user is admin, all he needs to do is call a function of `iFlyChatService` object and pass the user id of the user whose IP needs to be banned:
```
service.banIp(userId);
```
<br>
If some other admin has banned IP of some other user, everybody connected to the chat gets a broadcast about this event. iFlyChatLibrary sends a broadcast with user id of the user whose IP is banned, this broadcast intent have intent action named `iFlyChat.onUserBanIp` so that each client can update its view right away (although the updated global list will exclude that user given that the banned IP is not unbanned by the admin).

To listen to this broadcast and receive the event `iFlyChat.onUserBanIp`. The user needs to match the intent action in the application's `onReceive()` method. To retrieve the user id string. Firstly, user needs to create and initialize the Bundle type object `bundleData`. Then user can get `userId` string by calling `getString("userId")` method on data a Bundle type object :
```
if(intent.getAction().equals("iFlyChat.onUserBanIp")){
    Bundle bundleData = intent.getExtras();
    String userId = bundleData.getString("userId");
}
```
