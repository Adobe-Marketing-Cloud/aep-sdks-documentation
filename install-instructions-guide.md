# iOS install instructions guide

## Migration considerations 

Here are a few things to consider when installing the Adobe Experience Platform Edge Network mobile extension.

- The new AEP Edge Network extension requires the usage of the latest AEP SDKs, which for iOS is a new Swift-based SDK. If you are an ACP Mobile SDK user, read more about this in the [Adobe Experience Platform Edge Network Migration Considerations](../getting-started/introduction-to-aepedge.md#adobe-experience-platform-edge-network-migration-considerations).
- For the latest information on supported Swift SDK compatible extensions, see [Current SDK Versions](current-sdk-versions.md).
- This extension requires the use of [Identity for Edge Network mobile extension](../using-mobile-extensions/adobe-edge-identity).
- When using this extension, it is strongly encouraged to use Consent mobile extension for managing and enforcing the collect consent settings. For more details see [Consent extension](../using-mobile-extensions/adobe-edge-consent) and [Privacy and GDPR](../privacy-and-gdpr.md).

## Install the Swift AEP Mobile SDK extensions

### (Optional) Existing ACP users

Remove the Adobe pods prefixed with `ACP` from your Podfile so the Swift extensions can be installed in the following steps.

### Add the dependencies to the Podfile

Add the Mobile Core and Edge extensions to your project using Cocoapods. Add following pods in the `Podfile`:

```swift
use_frameworks!
target 'YourTargetApp' do
    // Mobile Core and dependents
    pod 'AEPCore'
    pod 'AEPSignal'
    pod 'AEPLifecycle'

    // Client-side user profile
    pod 'AEPUserProfile'

    // Edge Network and depenedents
    pod 'AEPEdge'
    pod 'AEPEdgeIdentity'
    pod 'AEPEdgeConsent'

    // Adobe Analytics and dependents
    pod 'AEPIdentity'
    pod 'AEPAnalytics'
end
```

This is just an example, check the full list of supported Swift SDK compatible extensions at [Current SDK Versions](current-sdk-versions.md). If you use additional extensions than the ones listed at [Current SDK Versions](current-sdk-versions.md), please contact your Adobe Customer Success Manager or account representative.

### Add initialization code

{% tabs %}
{% tab title="Swift" %}

```swift
// AppDelegate.swift

// Mobile Core and dependents
import AEPCore
import AEPSignal
import AEPLifecycle

// Client-side user profile
import AEPUserProfile

// Edge Network and depenedents
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent

// Adobe Analytics and dependents
import AEPIdentity
import AEPAnalytics
```

{% endtab %}

{% tab title="Objective-C" %}

```objective-c
// AppDelegate.h

// Mobile Core and dependents
@import AEPCore;
@import AEPSignal;
@import AEPLifecycle;

// Client-side user profile
@import AEPUserProfile;

// Edge Network and depenedents
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPEdgeConsent;

// Adobe Analytics and dependents
@import AEPIdentity;
@import AEPAnalytics;
```

{% endtab %}
{% endtabs %}

### Add extensions registration code

{% hint style="info" %}

Note that the registration setup changed to a single API call `MobileCore.registerExtensions([...])`. There is no need to call `MobileCore.start` anymore, registerExtensions does that implicitly.
{% endhint %}

{% tabs %}
{% tab title="Swift" %}

```swift
// AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([Signal.self, Lifecycle.self, UserProfile.self, Edge.self, AEPEdgeIdentity.Identity.self, Consent.self, AEPIdentity.Identity.self, Analytics.self], {
        MobileCore.configureWith(appId: "yourLaunchEnvironmentID")
    })
  ...
}
```

{% endtab %}

{% tab title="Objective-C" %}

```objective-c
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileSignal.class, AEPMobileLifecycle.class, AEPMobileUserProfile.class, AEPMobileEdge.class, AEPMobileEdgeIdentity.class, AEPMobileEdgeConsent.class, AEPMobileIdentity.class, AEPMobileAnalytics.class] completion:^{
    [AEPMobileCore configureWithAppId: @"yourLaunchEnvironmentID"];
  }];
  ...
}
```

{% endtab %}
{% endtabs %}

{% hint style="info" %}
Replace the string `yourLaunchEnvironmentID` with the value copied from the `Environment File ID` field, in the AEP Launch mobile install instructions.
{% endhint %}

## Partner extensions

If you are using any of the iOS partner extensions from the AEP Launch catalog, please contact your Adobe Customer Success Manager or account representative.