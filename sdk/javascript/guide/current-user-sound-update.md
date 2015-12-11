iFlyChat JavaScript SDK fires an event named '**current-user-sound-update**' whenever sound notification is switched on or off for current user. You may bind to this event in following manner:
~~~
iflychat.on('current-user-sound-update', function(message) {
  
  /* your code here - message object contains information about if sound is switched on or off */

});
~~~

Here message is a JS object with following properties:

* id
* sound

Possible values of sound:

* true - Sound is on/ Unmute
* false - Sound is Off/ Mute
