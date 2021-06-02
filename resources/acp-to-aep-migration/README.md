# Migrating to Swift

If you have implemented Objective-C versions \(ACP-prefixed SDK libraries, 2.x or lower\), then this guide will help you understand the steps required to migrate your implementation to the latest Swift versions \(AEP-prefixed SDK libraries, 3.x or higher\). In summary, you'll need to:

1. [Switch imported libraries from ACP-prefix to AEP-prefix libraries](./#switch-imported-libraries)
2. [Update SDK initialization](./#update-sdk-initialization)
3. [Update API references to call AEP-prefix libraries](./#update-api-usage-and-references-for-each-extension)

## Switch imported libraries

At this time, the following ACP-prefix libraries may be switched out with the respective AEP-prefix SDK libraries. See instructions on proceeding further if you have:

1. [Manually imported SDK libraries](./#manual-library-import) OR
2. [Cocoapods to manage SDK dependencies](./#cocoapods)

{% hint style="warning" %}
In addition to `ACPCore` being replaced with `AEPCore`, you will also need to explicitly import `AEPLifecycle`, `AEPIdentity`, and `AEPSignal` libraries to ensure no disruption in SDK behavior.
{% endhint %}

| ACP SDK | AEP SDK |
| :--- | :--- |
| ACPCore | AEPCore/AEPLifecycle/AEPIdentity/AEPSignal |
| ACPUserProfile | AEPUserProfile |
| ACPAnalytics | AEPAnalytics |
| ACPTarget | AEPTarget |
| ACPMedia | AEPMedia |
| ACPAudience | AEPAudience |

### Manual library import

If you are manually importing SDK libraries, ensure you identify all currently used ACP-prefix libraries and switch them over to AEP-prefix libraries. The list of current AEP-prefix SDK libraries are found [Current SDK Versions](../upgrading-to-aep/current-sdk-versions.md#ios-swift) \(in the Swift section\).

### Cocoapods

If you are using Cocoapods to manage your Adobe Experience Platform Mobile SDK dependencies, the following example shows you how to switch ACP-prefix libraries to AEP-prefix libraries in your `Podfile`.

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

Save the `Podfile` and run  `pod install`or `pod update` 

## Update SDK initialization

After you have imported the new Swift-based AEP-prefix libraries, you'll need to update SDK initialization code as described below. With Swift, the SDK has simplified initialization and registration of extensions to where the `MobileCore.start()` API is no longer required.

The following code snippets show the new and correct initialization code required for the Swift-based, AEP-prefix SDK libraries.

{% tabs %}
{% tab title="Objective-C" %}
```text
@import AEPCore;
@import AEPSignal;
@import AEPLifecycle;
@import AEPIdentity;
@import AEPUserProfile;
@import AEPServices;
...

// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
      [AEPMobileCore setLogLevel: AEPLogLevelDebug];
      [AEPMobileCore registerExtensions:@[AEPMobileSignal.class, AEPMobileLifecycle.class, AEPMobileUserProfile.class, AEPMobileIdentity.class] completion:^{
      [AEPMobileCore configureWithAppId: @"yourLaunchEnvironmentID"];
      [AEPMobileCore lifecycleStart:@{@"contextDataKey": @"contextDataVal"}];
    }];
    ...
}
```
{% endtab %}

{% tab title="Swift" %}
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

## Update API usage and references for each extension

Finally, you'll need to scan through your current implementation and replace ACP-prefix API calls to the new Swift-based, AEP-prefix libraries. A quick find and replace should do the trick. Detailed API changes by extension may be found at the links below.

* [Adobe Core extension](../../foundation-extensions/mobile-core/acpcore-aepcore.md)
* [Adobe Lifecycle extension](acplifecycle-aeplifecycle.md)
* [Adobe Signal extension](acpsignal-aepsignal.md)
* [Adobe UserProfile extension](acpuserprofile-aepuserprofile.md)

