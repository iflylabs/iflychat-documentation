#Ready-event#
iFlyChat JavaScript SDK fires an event named 'ready' when our app is ready. You may write your customisation code inside this event. You may bind to this event in following manner:
~~~
iflychat.on('ready', function(data) {
  
  /* your code here */

});
~~~

Please note that this event only fires once.
