# iOS App Extension Implementation

You can use supported Platform extensions in your App Extensions to collect usage data. Supported Adobe Extensions are shown [here](../../upgrading-to-aep/current-sdk-versions#ios-swift). This tutorial assumes a basic understanding of how to use the iOS SDK in applications.

## Adding the SDK

Adding the Mobile SDK to your App Extension works the same way as adding the Mobile SDK to your application. This tutorial explains installing the SDK using Cocoapods.

1. Add a new target in your podfile for your app extension, then add the Adobe pods to the newly added App Extension target in the podfile.

```
target 'YourApp' do
  pod 'AEPServices'
  pod 'AEPCore'
  pod 'AEPLifecycle'
  pod 'AEPIdentity'
  pod 'AEPAnalytics'
end

target 'YourAppExtension' do
  pod 'AEPServices'
  pod 'AEPCore'
  pod 'AEPLifecycle'
  pod 'AEPIdentity'
  pod 'AEPAnalytics'
end

```
2. Run `pod install` from the command line to install the pods to the App Extension target.

## Registering Extensions

Depending on the type of App Extension you are using, the registration and usage of the SDK will look different. Make sure you understand the lifecycle of your App Extension in order to know where best to register the SDK and call lifecycle start/pause. This tutorial will use the `ShareExtension` as the example.

1. Make sure that your `ShareViewController` has the proper imports for the SDK. 

```
import UIKit
import Social
import AEPCore
import AEPIdentity
import AEPAnalytics
import AEPLifecycle
```

2. Register the SDK in the `ShareViewController`'s `presentationAnimationDidFinish` method:

```
override func presentationAnimationDidFinish() {
        MobileCore.registerExtensions([Identity.self, Lifecycle.self, AnalyticsAppExtension.self], {
            MobileCore.configureWith(appId: "your-app-id")
            MobileCore.lifecycleStart(additionalContextData: nil)
        })
    }
```
Please note that in order to register AEPAnalytics, you must use the `AnalyticsAppExtension` class instead of the `Analytics` class used when registering from an application.

3. Managing lifeycle from a Share Extension should be done in the `didSelectCancel` and `didSelectPost` methods which are the delegate methods called when the ShareViewController is dismissed.

```
    override func didSelectCancel() {
        MobileCore.lifecyclePause()
    }

    override func didSelectPost() {
        MobileCore.lifecyclePause()
        ...
    }
```

You are now ready to use the SDK in your App Extension.

