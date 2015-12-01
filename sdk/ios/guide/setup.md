#Installation & Setup#

1. Copy the `iFlyChatLibrary.framework` file from the above link to your project. To do this, you just need to drag and drop the file to your project.


    ![Add iFlyChat Framework file](https://iflychat-website-iflylabs.netdna-ssl.com/sites/default/files/docs/sdk/ios/adding-iFlyChatLibrary-framework-file-documentation.gif)


2. Add `libicucore.tbd` file to your project.
    * Go to your application's target.
    * Go to `"General"` tab.
    * Under `"Linked frameworks and libraries"` add the above libraries using the plus button.

    ![Add libicucore.tbd file to project](https://iflychat-website-iflylabs.netdna-ssl.com/sites/default/files/docs/sdk/ios/adding-library-to-iFlyChat-example-application-documentation.gif)  
  
3. Import the `“iFlyChatLibrary/iFlyChatlibrary.h”` file wherever you want to use the chat service functions.

    ```
    #import "iFlyChatLibrary/iFlyChatLibrary.h"
    ```
    
    Note: In a Swift iOS project, one will need to create an Objective-C bridging header to be able to import the framework's header file.

       * Create an Objective-C header file in your project and import the `iFlyChatLibrary.h` file there.


       * Add the relative path of this header file in the `"Build Settings"` of your project's target under `Objective-C Bridging Header` option.

           ![Adding relative path to build settings](https://iflychat-website-iflylabs.netdna-ssl.com/sites/default/files/docs/sdk/ios/adding-bridging-header-setting-documentation.gif)

##Precautions to be taken.

1. Make sure that in your application target's `Build Settings`, under `"Framework Search Path"`, the framework's path is mentioned. To avoid any problem, it is recommended to copy the framework file while linking.

2. iOS 9's `App Transport Security` does not allow for "http" connections. To work around it, you may add an exception in the `Info.plist` file in the main <dict> tag like so:

    ```
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
    ```

    or if you need to allow all "http" connections, you may write the following code:

    ```
    <key>NSAppTransportSecurity&lt;/key>  
         <dict>  
              <key>NSAllowsArbitraryLoads</key><true/>  
         </dict>
    ```
  
3. Set `"ENABLE_BITCODE"` to NO in Application target's `Build Settings` when testing on a device.
