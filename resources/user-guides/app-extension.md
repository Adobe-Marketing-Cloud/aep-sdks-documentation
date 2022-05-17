# iOS App Extension Implementation

You can use supported AEP extensions in your App Extensions to collect usage data. Supported Adobe Extensions are shown [here](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions#ios-swift). This tutorial assumes a basic understanding of how to use the iOS SDK in applications.

## Adding the SDK

Getting the Mobile SDK in your App Extension works the same way as for your application. For this tutorial we will go over Cocoapods as the method of installing the SDK.

1. First, simply add a new target in your podfile for your app extension, then add the Adobe pods to the newly added App Extension target in the podfile.

E.g:
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

Depending on the type of App Extension you are using, the registration and usage of the SDK will look different. Make sure you understand the lifecycle of your App Extension in order to know where best to register the SDK and call lifecycle start/pause. For this tutorial we will be using the ShareExtension as the example.

1. Make sure that your `ShareViewController` has the proper imports for the SDK. 
E.g:

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

You are now ready to use the SDK in your App Extension

