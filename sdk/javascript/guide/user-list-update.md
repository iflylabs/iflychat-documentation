iFlyChat JavaScript SDK fires an event named '**user-list-update**' whenever user list is updated. You may bind to this event in following manner:
~~~
iflychat.on('user-list-update', function(data) {
  
  /* your code here - data object contains user list information */

});
~~~

Here data is a JS object with following properties:

* type
* id
* users
* rooms