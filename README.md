moves-ios-sdk
=============
Moves App SDK For iOS. 

[Official API Documents](https://dev.moves-app.com/)

#Getting Started

##Installing the moves-ios-sdk
###1.CocoaPods
If you use [CocoaPods](http://cocoapods.org/), you can add the ``moves-ios-sdk`` pod to your Podfile. Then run ``pod install``, and the Moves SDK will be available in your project. See the documentation on the CocoaPods website if you want to set up a new or existing project.
###2.Add the moves-ios-sdk to your project
- Open your existing project.
- Drag the **moves-ios-sdk** folder from the example project into your Xcode project.
- Make sure the “Copy items into destination group’s folder (if needed)” checkbox is checked.
- In this case you need to add [AFNetworking](https://github.com/AFNetworking/AFNetworking) to your project

##Get ClientId and ClientSecret
When you register your app with Moves, it will provide you with a **Client ID** and **Client secret**. They identify your app to Moves's API. 

[Register your app with Moves](https://dev.moves-app.com/clients)

##Add the Moves URL scheme
copy and paste the following into the XML Source for the Info.plist:

    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.yourcompany</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>[YOUR URL SCHEME]</string>
            </array>
        </dict>
    </array>
**[YOUR URL SCHEME]** is set when you [Register your app with Moves](https://dev.moves-app.com/clients)

##Configure your App Delegate

At the top of your app delegate source file (and anywhere you call the MovesAPI object), you'll need to include the ``MovesAPI.h``.  Simply add this line:

``#import "MovesAPI.h"``

###In AppDelegate. Set Your [Client ID],[Client secret] and [Redirect URI]

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
        [[MovesAPI sharedInstance] setShareMovesOauthClientId:@"[YOUR Client ID]"
                                            oauthClientSecret:@"[YOUR Client secret]"
                                            callbackUrlScheme:@"[YOUR URL SCHEME]"];
        return YES;
    }
###Add handle Url method
The final step is to give the SDK an opportunity to handle incoming URLs. 
 
    - (BOOL)application:(UIApplication *)application handleOpenURL:(NSURL *)url {
        if ([[MovesAPI sharedInstance] canHandleOpenUrl:url]) {
            return YES;
        }
        // Other 3rdParty Apps Handle Url Method...
        
        
        return NO;
    }

#Authorization 
    [[MovesAPI sharedInstance] authorizationSuccess:^{
        // Auth successed! Now you can get Moves's data
    } failure:^(NSError *reason) {
        // Auth failed!
    }];

#Start get Moves's data
Get user profile

    [[MovesAPI sharedInstance] getUserSuccess:^(MVUser *user) {
        // Get user
    } failure:^(NSError *error) {
        // Something wrong
    }];

More other API see the ``MovesAPI.h`` file
#Acknowledgements
The **moves-ios-sdk** uses the following open source software:

- [AFNetworking](https://github.com/AFNetworking/AFNetworking)

#License

See the [MIT license](https://github.com/vitoziv/moves-ios-sdk/blob/master/LICENSE).
