#Error handling

There are various errors that the iFlyChatLibrary throws while performing some operations. For this purpose, the iFlyChatLibrary creates an `iFlyChatError` object and sends it with a notification named `"iFlyChat.onError"`.

To listen to this notification and receive the `onError` event, the user needs to add observer to the application and retrieve the `iFlyChatError` object from the notification:

~~~
//OBJECTIVE-C

[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onError:) name:@”iFlyChat.onError” object:nil];

-(void) onError:(NSNotification *)notification
{
    iFlyChatError *error = [notification object];
    NSString *code = [error getErrorCode];
    NSString *message = [error getErrorMessage];
    NSString *source = [error getErrorSource];
}
~~~

~~~
//SWIFT

NSNotificationCenter.defaultCenter().addObserver
(
    self,
    selector: "onError:",
    name: "iFlyChat.onError",
    object: nil
)

func onError(notification: NSNotification)
{
    let error: iFlyChatError = notification.object! as! iFlyChatError
    let code:NSString = error.getErrorCode() as! NSString
    let message:NSString = error.getErrorMessage() as! NSString
    let source:NSString = error.getErrorSource() as! NSString
}
~~~

For more details on which errors are thrown, their error codes, error messages and error sources, see iFlyChatError.h file from `iFlyChatLibrary.framework`.