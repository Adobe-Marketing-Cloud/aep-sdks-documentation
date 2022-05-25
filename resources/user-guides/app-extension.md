# iOS App Extension implementation

You can use supported Adobe Experience Platform mobile extensions in your App Extensions to collect usage data. The supported AEP mobile extensions are listed [here](../upgrading-to-aep/current-sdk-versions.md#ios--swift). 

## Prerequisites

- This tutorial assumes a basic understanding of how to use the iOS AEP Mobile SDK in applications. For more details see [Getting Started](../../getting-started/overview.md).
- You should have CocoaPods installed.

## Adding the AEP mobile extensions

Adding the Mobile SDK to your App Extension works the same way as adding the Mobile SDK to your application.

1. In the Podfile, add a new target for your app extension and include the Adobe pods:

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

This tutorial uses the `ShareExtension` as the example.

{% hint style="info" %}
Depending on the type of App Extension you are using, the registration and usage of the SDK will look different. Make sure you understand the lifecycle of your App Extension in order to know where best to register the SDK and call lifecycle start/pause. 
{% endhint %}

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

### Swift

```swift
override func presentationAnimationDidFinish() {
        MobileCore.registerExtensions([Identity.self, Lifecycle.self, AnalyticsAppExtension.self], {
            MobileCore.configureWith(appId: "your-app-id")
            MobileCore.lifecycleStart(additionalContextData: nil)
        })
    }
```

{% hint style="info" %}
Please note that in order to register AEPAnalytics, you must use the `AnalyticsAppExtension` class instead of the `Analytics` class used when registering from an application.
{% endhint %}

3. Managing lifeycle from a Share Extension should be done in the `didSelectCancel` and `didSelectPost` methods which are the delegate methods called when the ShareViewController is dismissed.

### Swift

```swift
    override func didSelectCancel() {
        MobileCore.lifecyclePause()
    }

    override func didSelectPost() {
        MobileCore.lifecyclePause()
        ...
    }
```

You are now ready to use the SDK in your App Extension.

