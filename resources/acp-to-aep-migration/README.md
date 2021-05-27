# Migrating from ACP (Objective-C) SDK to AEP (Swift) SDK

We suggest the following general process when migrating from ACP SDK to AEP SDK in a mobile app:

### Update the Podfile

Replace the dependencies in your `Podfile` for SDK extensions, using core extensions and profile extension as an example:

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

The supported `pod`s to be replaced:

| ACP SDK        | AEP SDK                                     |
| -------------- | ------------------------------------------- |
| ACPCore        | AEPCore/AEPLifecycle/AEPIdentity/AEPSignal  |
| ACPUserProfile | AEPUserProfile                              |
| ACPAnalytics   | AEPAnalytics                                |
| ACPTarget      | AEPTarget                                   |
| ACPMedia       | AEPMedia                                    |
| ACPAudience    | AEPAudience                                 |

Save the `Podfile` and run the install command:

```shell
pod install
```

### Update the initialization code

The following code snippets show the difference in the initialization code between ACP and AEP SDKs. The AEP SDK has changed the way of registering extensions and has gotten rid of calling the `MobileCore.start()` API.

{% tabs %} 

{% tab title="Objective-C" %} 

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

- AEP SDK

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

{% endtab %}

{% tab title="Swift" %} 

- ACP SDK

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

- AEP SDK

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

{% endtab %}

{% endtabs %}

### Update API usage for each extension

The following documents detail API changes between ACP SDKs and AEP SDKs.

- [Adobe Core extension](ACPCore-AEPCore.md)

- [Adobe Lifecycle extension](ACPLifecycle-AEPLifecycle.md)

- [Adobe Signal extension](ACPSignal-AEPSignal.md)

- [Adobe UserProfile extension](ACPUserProfile-AEPUserProfile.md)

  
