iFlyChat JavaScript SDK has a function named '**startChat**' which can be used to start chat with a specific user or join a room. You may use the function in the following manner:
~~~
iflychat.startChat({
  
  id: '1', /* id of the user or room with whom to start chat */
  name: 'admin', /*name of the user or room with whom to start chat */
  state: 'open' /* defines if chat needs to be started in open state or minimised state*/

});
~~~

This function takes a JS object as paramter which should have following properties:

* id
* name
* state

Possible values of parameters :

* state: 'open' ,  'minimised'
