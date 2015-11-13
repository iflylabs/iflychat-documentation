**Error Handling**

Whenever an error occurs while executing a method from iFlyChatLibrary SDK, an intent will be broadcasted with an iFlyChatError object. To test the working of your app with iFlyChatLibrary SDK, you need to add iFlyChat.onError action to your intent filter in onStart() method. 

To listen to this broadcast and receive the event(iFlyChat.onError), the user needs to match the intent action in the application's onReceive() method. To retrieve the iFlyChatError object, the user needs to create and initialize the Bundle type object (bundleData) and then the user can get iFlyChatError object by calling getParceleable("error") method on bundleData a Bundle type object :
<code>
if(intent.getAction().equals("iFlyChat.onError")){
    Bundle bundleData = intent.getExtras();
    iFlyChatError error = bundleData.getParcelable("error");
    Log.e("iFlyChat.onError","Error code is: " + error.getCode() + " with message: " 
    + error.getMessage() + " and source: " + error.getSource());
}
</code>
<br>

There are several getter methods which returns some properties of the iFlyChatError object like iFlyChatLibrary generated error codes, reason of error and class and method where error has occurred. These getter methods are explained in the documentation of the iFlyChatLibrary.

<br>

**Debugging**

To help you debug fast, several logs are set on constructors, methods and while broadcasting intents. These logs will tell whether a constructor or method resulted in success or an error or if an intent is about to be broadcasted. 

To enable debugging in iFlyChatLibrary, you need to call setIsDebug(true) method of the Utilities class of iFlyChatLibrary. By default it is set to false.
<code>
Utilities.setIsDebug(true);
</code>
<br>
To see the successful logs in logcat of android studio, user can select log level as "info".

To see the unsuccessful/error logs in logcat of android studio, user can select log level as "Error".
