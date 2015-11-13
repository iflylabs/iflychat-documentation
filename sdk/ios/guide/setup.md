#Installation & Setup#

1. Copy the <font color='blue'>iFlyChatLibrary.framework</font> file from the above link to your project. To do this, you just need to drag and drop the file to your project.


    ![Add iFlyChat Framework file](https://lh5.googleusercontent.com/-6es2W67Wf7k/VgEhAewx7HI/AAAAAAAAA0w/mLWhUWTPfDw/w804-h540-no/Adding%2BiFlyChatLibrary%2BFramework%2Bfile.gif)


2. Add <font color='blue'>libicucore.tbd</font> file to your project.
    * Go to your application's target.
    * Go to <font color='blue'>"General"</font> tab.
    * Under <font color='blue'>"Linked frameworks and libraries"</font> add the above libraries using the plus button.

    ![Add libicucore.tbd file to project](https://lh3.googleusercontent.com/-Jf1cnedJjIA/VgEhAYg_ltI/AAAAAAAAA0w/K0shr0R0Gyc/w804-h540-no/Adding%2BLibrary%2Bto%2BiFlyChat%2BExample%2BApplication.gif)  
  
3. Import the <font color='blue'>“iFlyChatLibrary/iFlyChatlibrary.h”</font> file wherever you want to use the chat service functions.

    <code>
    #import "iFlyChatLibrary/iFlyChatLibrary.h"</code>  
    Note: In a Swift iOS project, one will need to create an Objective-C bridging header to be able to import the framework's header file.

       * Create an Objective-C header file in your project and import the <font color='blue'>iFlyChatLibrary.h</font> file there.


       * Add the relative path of this header file in the <font color='blue'>"Build Settings"</font> of your project's target under <font color='blue'>Objective-C Bridging Header</font> option.

           ![Adding relative path to build settings](https://lh3.googleusercontent.com/-4B-7-ONrNs8/VgEizogwXzI/AAAAAAAAA1M/trXPn3kHlVk/w804-h540-no/Adding%2BBridging%2BHeader%2BSetting.gif)

##Precautions to be taken.

1. Make sure that in your application target's <font color='blue'>Build Settings</font>, under <font color='blue'>"Framework Search Path"</font>, the framework's path is mentioned. To avoid any problem, it is recommended to copy the framework file while linking.

2. iOS 9's <font color='blue'>App Transport Security</font> does not allow for "http" connections. To work around it, you may add an exception in the <font color='blue'>Info.plist</font> file in the main <dict> tag like so:

    <code>
    <key>NSAppTransportSecurity&lt;/key>  
    <dict>  
          <key>NSAllowsArbitraryLoads</key>  
          <false/>  
           <key>NSExceptionDomains</key>  
           <dict>  
                <key>yourdomain.com</key>  
                <dict>  
                    <key>NSIncludesSubdomains</key>  
                    <true/>  
                    <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>  
                    <true/>  
                    <key>NSTemporaryExceptionMinimumTLSVersion</key>  
                    <string>TLSv1.1</string>  
                </dict>  
           </dict>  
    </dict>  
    

    or if you need to allow all "http" connections, you may write the following code:

    <key>NSAppTransportSecurity&lt;/key>  
         <dict>  
              <key>NSAllowsArbitraryLoads</key><true/>  
         </dict>
    </code>  
  
3. Set <font color='blue'>"ENABLE_BITCODE"</font> to NO in Application target's <font color='blue'>Build Settings</font> when testing on a device.