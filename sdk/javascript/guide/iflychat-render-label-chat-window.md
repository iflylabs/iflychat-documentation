iFlyChat JavaScript SDK has a function named '**renderLabelInChatWindow**' which can be used to add custom label to chat window. You may use the function in the following manner:
~~~
iflychat.renderLabelInChatWindow({
  
  id: 'c-0', /* id of the chat room or user */
  position: 'above-chat-content', /* position of the label */
  content: 'This is a custom header in the chat window' /* label content */

});
~~~

This function takes a JS object as parameter which should have following properties:

| Property | Description                                                                                            |
|----------|--------------------------------------------------------------------------------------------------------|
| id       | id of the chat room or window                                                                          |
| position | position of the label inside chat window. Possible values are above-chat-content or below-chat-content |
| content  | content of the label                                                                                   |
