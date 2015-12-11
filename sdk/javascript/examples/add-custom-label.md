You can add a custom label in chat window by using our iFlyChat JavaScript SDK. This would allow you to add your own content inside the chat window either in header or footer. It can be used for declaring chat rules and regulations or for showing advertisements.

We have a function named [iflychat.renderLabelInChatWindow](https://iflychat.com/docs/sdk/javascript/reference/iflychat.renderLabelInChatWindow/v1.0) in JS SDK for this purpose. It takes an object as parameter which should have following properties:

* id
* position
* content
 

An example is shown below:
~~~
window.iflychatAsyncInit = function() {
  
  // All iFlyChat related code should be defined here
  
  /** iFlyChat Init function **/

  iflychat.init({
  
    userlist : {
      visible: true
    }

  });

  /** iFlyChat ready event **/
  iflychat.on('ready', function() {

    var htmlContent = '<div style="padding:2px;">';
    htmlContent += 'This is a custom label above the chat window.';
    htmlContent += '<div style="color:red;">';
    htmlContent += 'You can also customise look and feel.';
    htmlContent += '</div>';
    htmlContent += '</div>'; 
    
    iflychat.renderLabelInChatWindow({ 
      id: 'c-0', 
      position: 'above-chat-content', 
      content: htmlContent 
    }); 
  }); 
};
~~~

Please note that you should be using [Enterprise](https://iflychat.com/enterprise-plans) plan in order to be able to use this feature.

It will look like this:

![Image of Chat Window](https://iflychat-website-iflylabs.netdna-ssl.com/sites/default/files/images/kb/how-to-add-custom-label-in-chat-window.png)