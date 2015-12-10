iFlyChat JavaScript SDK fires an event named '**current-user-status-update**' whenever status of current user is update. You may bind to this event in following manner:
~~~
iflychat.on('current-user-status-update', function(message) {
  
  /* your code here - message object contains status information */

});
~~~

Here message is a JS object with following properties:

* id
* status
Possible values of status:

* '1' - Available
* '2' - Idle
* '3' - Busy
* '4' - Sign Out