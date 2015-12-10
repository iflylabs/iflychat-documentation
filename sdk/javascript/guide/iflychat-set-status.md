iFlyChat JavaScript SDK has a function named '**setStatus**' which can be used to set the status of current user. You may use the function in the following manner:
~~~
iflychat.setStatus({
  
  status: '1' /*status which needs to be set */

});
~~~

This function takes a JS object as paramter which should have following properties:

* status
Possible values of status are :

* '1' - Available 
* '2' - Idle 
* '3' - Busy
* '4' - Sign Out    