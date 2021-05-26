# Migrating from ACP (Objective-C) SDK to AEP (Swift) SDK

We suggest the following general process when migrating from ACP SDK to AEP SDK in a mobile app:

### Update the Podfile

Replace the (extension) dependencies in your `Podfile`, using core extensions and profile extension as an example:

```ruby
# replace ACPCore with AEPCore/AEPLifecycle/AEPIdentity/AEPSignal
# pod 'ACPCore'
  pod 'AEPCore'
  pod 'AEPLifecycle'
  pod 'AEPIdentity'
  pod 'AEPSignal'

# replace ACPUserProfile with AEPUserProfile
# pod 'ACPUserProfile'
	pod 'AEPUserProfile'
```

The supported `pod`s  to be replaced:

| ACP SDK        | AEP SDK                                     |
| -------------- | ------------------------------------------- |
| ACPCore        | AEPCore/ AEPLifecycle/AEPIdentity/AEPSignal |
| ACPUserProfile | AEPUserProfile                              |
| ACPAnalytics   | AEPAnalytics                                |
| ACPTarget      | AEPTarget                                   |
| ACPMedia       | AEPMedia                                    |
| ACPAudience    | AEPAudience                                 |
|                |                                             |
|                |                                             |
|                |                                             |

Save the `Podfile` and run the install command:

```shell
pod install
```

### Update initialization code

The following code snippets show the difference in initialization code between ACP and AEP SDKs. The AEP SDK has changed the way of registering extensions and has gotten rid of calling the `start()` API.

#### Objective-C

- ACP SDK

```objective-c
#import "AppDelegate.h"
#import "ACPCore.h"
#import "ACPUserProfile.h"
#import "ACPIdentity.h"
#import "ACPLifecycle.h"
#import "ACPSignal.h"
...
  
@implementation AppDelegate
-(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPCore setLogLevel:ACPMobileLogLevelDebug];
  [ACPCore configureWithAppId:@"<your_environment_id_from_Launch>"];
  [ACPUserProfile registerExtension];
  [ACPIdentity registerExtension];
  [ACPLifecycle registerExtension];
  [ACPSignal registerExtension];
  [ACPCore start:^{
    [ACPCore lifecycleStart:nil];
  }];
  ...
  return YES;
}
...
@end
```

```objective-c
#import <AEPCore/AEPCore.h>
#import <AEPSignal/AEPSignal.h>
#import <AEPLifecycle/AEPLifecycle.h>
#import <AEPIdentity/AEPIdentity.h>
#import <AEPServices/AEPServices.h>
...
  
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileSignal.class, AEPMobileLifecycle.class, AEPMobileUserProfile.class, AEPMobileIdentity.class] completion:^{
    [AEPMobileCore configureWithAppId: @"yourLaunchEnvironmentID"];
    [AEPMobileCore lifecycleStart:@{@"contextDataKey": @"contextDataVal"}];
  }];
  ...
}
```

##### Swift

```swift
import ACPCore
import ACPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
  func application(_application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool{
		    ACPCore.setLogLevel(.debug)
        ACPCore.configure(withAppId: "<your_environment_id_from_Launch>")
		    ACPUserProfile.registerExtension()
        ACPIdentity.registerExtension()
        ACPLifecycle.registerExtension()
        ACPSignal.registerExtension()
        ACPCore.start {
        	ACPCore.lifecycleStart(nil)
        }
    ...
    return true
  }
}

@end
```

```swift
// AppDelegate.swift
import AEPCore
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPUserProfile

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([Signal.self, Lifecycle.self, UserProfile.self, Identity.self], {
        MobileCore.configureWith(appId: "yourLaunchEnvironmentID")
      	MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
    })
  ...
}
```

### Update API usage for each extensions

The following documents detail API changes between ACP SDKs and AEP SDKs.

- Adobe Core extension APIs

- Adobe Lifecycle extension APIs

- Adobe Signal extension APIs

- Adobe UserProfile extension APIs

  