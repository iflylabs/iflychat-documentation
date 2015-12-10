**Steps to integrate iFlyChatLibrary to Android project**

iFlyChat provides it's JavaScript SDK which can be used to customize chat and bind to various chat related events.

You may bind to our init event by using the following code:
~~~
window.iflychatAsyncInit = function() {
  
  // All iFlyChat related code should be defined here
  
  /** iFlyChat Init function **/

  iflychat.init({
  
    userlist : {
      visible: true
    }

  });

  /** iFlyChat ready event **/
  iflychat.on('ready', function() {
    
    // Write your custom iFlyChat related code here

  }); 

};
~~~

It is fired when chat starts initialising. 

Note that you should be using a [premium plan](https://iflychat.com/pricing) in order to be able to use this feature.
