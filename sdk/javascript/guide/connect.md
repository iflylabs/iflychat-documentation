iFlyChat JavaScript SDK fires an event named '**connect**' whenever the app has connected to our cloud network. You may bind to this event in following manner:
~~~
iflychat.on('connect', function(data) {

  /* your code here */

});
~~~

Please note that this event may fire more than once if the chat is disconnected and then re-connected.
