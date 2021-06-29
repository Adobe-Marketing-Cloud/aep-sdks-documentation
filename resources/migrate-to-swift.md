# Migrate to Swift

If you have implemented Objective-C versions \(ACP-prefixed SDK libraries, 2.x or lower\), then this guide will help you understand the steps required to migrate your implementation to the latest Swift versions \(AEP-prefixed SDK libraries, 3.x or higher\). In summary, you'll need to:

1. [Switch imported libraries from ACP-prefix to AEP-prefix libraries](migrate-to-swift.md#switch-imported-libraries)
2. [Update SDK initialization](migrate-to-swift.md#update-sdk-initialization)
3. [Update API references to call AEP-prefix libraries](migrate-to-swift.md#update-api-usage-and-references-for-each-extension)

## Switch imported libraries

At this time, the following ACP-prefix libraries may be switched out with the respective AEP-prefix SDK libraries. See instructions on proceeding further if you have:

1. [Manually imported SDK libraries](migrate-to-swift.md#manual-library-import) OR
2. [Cocoapods to manage SDK dependencies](migrate-to-swift.md#cocoapods)

{% hint style="warning" %}
In addition to `ACPCore` being replaced with `AEPCore`, you will also need to explicitly import `AEPLifecycle`, `AEPIdentity`, and `AEPSignal` libraries to ensure no disruption in SDK behavior.
{% endhint %}

| Objective-C \(ACP-prefix\) | Swift \(AEP-prefix\) |
| :--- | :--- |
| ACPCore | AEPCore/AEPLifecycle/AEPIdentity/AEPSignal |
| ACPUserProfile | AEPUserProfile |
| ACPAnalytics | AEPAnalytics |
| ACPAudience | AEPAudience |
| ACPTarget | AEPTarget |
| ACPMedia | AEPMedia |
| ACPPlaces | AEPPlaces |
| ACPCampaign | AEPCampaign |

### Manual library import

If you are manually importing SDK libraries, ensure you identify all currently used ACP-prefix libraries and switch them over to AEP-prefix libraries. The list of current AEP-prefix SDK libraries are found [Current SDK Versions](upgrading-to-aep/current-sdk-versions.md#ios-swift) \(in the Swift section\).

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

Save the `Podfile` and run `pod repo update` to update your local Cocoapods repository.

Once the previous command is complete, run `pod install` or `pod update` to update the application dependencies.

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

| SDK Component & Extensions | Migration API Reference |
| :--- | :--- |
| [Core](../foundation-extensions/mobile-core/) | [AEPCore](../foundation-extensions/mobile-core/acpcore-aepcore.md) |
| [Lifecycle](../foundation-extensions/mobile-core/lifecycle/) | [AEPLifecycle](../foundation-extensions/mobile-core/lifecycle/acplifecycle-aeplifecycle.md) |
| [Signal](../foundation-extensions/mobile-core/signals/) | [AEPSignal](../foundation-extensions/mobile-core/signals/acpsignal-aepsignal.md) |
| [Profile](../foundation-extensions/profile/) | [AEPUserProfile](../foundation-extensions/profile/acpuserprofile-aepuserprofile.md) |
| [Adobe Experience Platform Places Service](../foundation-extensions/places/) | [AEPPlaces](../foundation-extensions/places/migration.md) |
| [Adobe Analytics - Mobile Services](../using-mobile-extensions/adobe-analytics-mobile-services/) | [AEPMobileService](../using-mobile-extensions/adobe-analytics-mobile-services/migration.md) |
| [Adobe Experience Platform Campaign](../using-mobile-extensions/adobe-campaign-standard/) | [AEPCampaign](../using-mobile-extensions/adobe-campaign-standard/migration.md) |

