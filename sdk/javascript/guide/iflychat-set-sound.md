iFlyChat JavaScript SDK has a function named '**setSound**' which can be used to mute/unmute the chat notification of current user. You may use the function in the following manner:
~~~
iflychat.setSound({
  
  sound: true /*If sound notification needs to set on or off */

});
~~~

This function takes a JS object as paramter which should have following properties:

* sound

Possible values of status are :

* true - Sound On/ Unmute
* false - Sound Off/ Mute
