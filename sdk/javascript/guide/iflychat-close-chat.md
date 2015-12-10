iFlyChat JavaScript SDK has a function named '**closeChat**' which can be used to close chat with a specific user or leave a room. You may use the function in the following manner:
~~~
iflychat.closeChat({

  id: '1', /* id of the user or room with whom to close chat */
  name: 'admin' /*name of the user or room with whom to close chat */

});
~~~

This function takes a JS object as parameter which should have following properties:

* id
* name