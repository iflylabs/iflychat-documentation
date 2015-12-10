iFlyChat JavaScript SDK has a function named '**minimiseChat**' which can be used to minimise chat window of a specific user room. You may use the function in the following manner:
~~~
iflychat.minimiseChat({
  
  id: '1', /* id of the user or room */
  name: 'admin' /*name of the user or room */

});
~~~

This function takes a JS object as parameter which should have following properties:

* id
* name