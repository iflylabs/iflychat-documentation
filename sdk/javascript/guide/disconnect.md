iFlyChat JavaScript SDK fires an event named '**disconnect**' whenever the app has disconnected from our cloud network. You may bind to this event in following manner:
~~~
iflychat.on('disconnect', function(data) {

  /* your code here */

});
~~~

Please note that this event may fire more than once if the chat is disconnected and then re-connected.