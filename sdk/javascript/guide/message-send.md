iFlyChat JavaScript SDK fires an event named 'message-send' whenever a new message is sent by the current user. You may bind to this event in following manner:
~~~
iflychat.on('message-send', function(message) {
  
  /* your code here - message object contains received message information */

});
~~~

Here message is a JS object with following properties:

* fromId
* fromName
* toId
* toName
* message
* messageId
