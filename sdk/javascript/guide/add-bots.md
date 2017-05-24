iFlyChat JavaScript SDK has a function named '**addBots**' which can be used to add bots to userlist.You may use the function in the following manner:
~~~
    var bots = [
    {"name":"neil","avatar":"https://cdn.pixabay.com/photo/2014/12/22/00/07/tree-576847_960_720.png","profileUrl":"www.iflychat.com/user/neil"},
    {"name":"jon","avatar":"https://cdn.pixabay.com/photo/2014/12/22/00/07/tree-576847_960_720.png","profileUrl":"www.iflychat.com/user/jon"}
    ];
    window.iflychatAsyncInit = function() {
      /** iFlyChat ready event **/
      iflychat.on('ready', function() {
        // Write your custom iFlyChat related code here
        iflychat.addBots(bots);
      });
    };
~~~

This function takes an Array of objects as parameter where each object should have following properties:

* name - Name of the bot you want to assign.
* avatar - Avatar url.
* profileUrl - Link of bot profile.