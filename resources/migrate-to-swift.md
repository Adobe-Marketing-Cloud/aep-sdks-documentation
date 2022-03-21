# Migrate to Swift

If you have implemented Objective-C versions \(ACP-prefixed SDK libraries, 2.x or lower\), then this guide will help you understand the steps required to migrate your implementation to the latest Swift versions \(AEP-prefixed SDK libraries, 3.x or higher\). In summary, you'll need to:

1. [Switch imported libraries from ACP-prefix to AEP-prefix libraries](migrate-to-swift.md#switch-imported-libraries)
2. [Update SDK initialization](migrate-to-swift.md#update-sdk-initialization)
3. [Update API references to call AEP-prefix libraries](migrate-to-swift.md#update-api-usage-and-references-for-each-extension)

## Switch imported libraries

At this time, the following ACP-prefix libraries may be switched out with their respective AEP-prefix SDK libraries. See instructions on proceeding further if you have [manually imported SDK libraries](migrate-to-swift.md#manual-library-import) , if you used [CocoaPods to manage SDK dependencies](migrate-to-swift.md#cocoapods), or you used [Swift Package Manager](migrate-to-swift.md#swift-package-manager).

{% hint style="warning" %}
In addition to `ACPCore` being replaced with `AEPCore`, you will also need to explicitly import `AEPLifecycle`, `AEPIdentity`, and `AEPSignal` libraries to ensure there is no disruption in SDK behavior.
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
| AEPAssurance \(1.x\) | AEPAssurance \(3.x\) |
| ACPCampaign | AEPCampaign |

### Manual library import

If you are manually importing SDK libraries, ensure you identify all currently used ACP-prefix libraries and switch them over to AEP-prefix libraries. The list of current AEP-prefix SDK libraries can be found in the [current SDK versions document](upgrading-to-aep/current-sdk-versions.md#ios-swift) \(in the Swift section\).

### CocoaPods

If you are using CocoaPods to manage your Adobe Experience Platform Mobile SDK dependencies, the following example shows you how to switch ACP-prefix libraries to AEP-prefix libraries in your `Podfile`.

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

Save the `Podfile` and run `pod repo update` to update your local CocoaPods repository.

Once the previous command is complete, run `pod install` or `pod update` to update the application dependencies.

### Swift Package Manager

#### Swift Package Collection

In Swift 5.5, the Swift Package Manager (SPM) adds support for [package collections](https://www.swift.org/blog/package-collections). You can configure package collection in Xcode 13 for easy installation of AEP SDKs. The Swift package collection for the Adobe Experience Platform SDKs is available at the [Adobe Open Source site](https://opensource.adobe.com/aepsdk-core-ios/swift/packages/aep.json).

To add the Swift package collection in Xcode 13, select File followed by Add Packages", selecting the plus sign on the bottom left and choosing "Add Swift Package Collection"

![](../.gitbook/assets/spm-add-package-collection.png)

Next, enter the package collection URL and click "Load". After the package collection has loaded, click "Add Collection" to add the collection.

![](../.gitbook/assets/spm-add-package-collection-load.png)

You should now see the added package collection on the left pane. Once selected, you will see all of the packages included in the collection listed.

![](../.gitbook/assets/spm-package-collection-aep.png)


#### Installing AEP SDKs using SPM 

To add the AEP SDK Packages to your application, from the Xcode 13 menu select:

```
File > Add Packages...
```

If you have configured package collection as mentioned above, select each package you would like to add to your project and click "Add Package" on the bottom right.

If not, enter the Package URL for the AEP SDK repositories: 

- AEPCore: `https://github.com/adobe/aepsdk-core-ios.git`
- AEPUserProfile: `https://github.com/adobe/aepsdk-userprofile-ios.git`

For each package, specify the Dependency rule as a specific version or a range of versions and select the Project. 

When prompted, select all the `AEP*` libraries, then click `Add Package`.


Alternatively, if your project has a `Package.swift` file, you can add AEPCore and AEPUserProfile directly to your dependencies:

```ruby
dependencies: [
    .package(url: "https://github.com/adobe/aepsdk-core-ios.git", .upToNextMajor(from: "3.0.0")),
    .package(url: "https://github.com/adobe/aepsdk-userprofile-ios.git", .upToNextMajor(from: "3.0.0")),
],
targets: [
    .target(name: "YourTarget",
            dependencies: [
                .product(name: "AEPCore", package: "AEPCore"),
                .product(name: "AEPIdentity", package: "AEPCore"),
                .product(name: "AEPSignal", package: "AEPCore"),
                .product(name: "AEPLifecycle", package: "AEPCore"),
                .product(name: "AEPServices", package: "AEPCore"),
                .product(name: "AEPUserProfile", package: "AEPUserProfile"),
            ],
            path: "your/path"),
]
```

## Update SDK initialization

After you have imported the new Swift-based AEP-prefix libraries, you'll need to update SDK initialization code as described below. With Swift, the `MobileCore.start()` API is no longer required. The SDK has simplified initialization and registration of extensions by providing the `MobileCore.registerExtensions()` API. After the given extensions have been registered, the SDK will be initialized and the completion block will be executed. Code which used to reside in the start\(\) block will now reside in the `MobileCore.registerExtensions()` completion block.

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
@import AEPAssurance;
...

// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
      [AEPMobileCore setLogLevel: AEPLogLevelDebug];
      [AEPMobileCore registerExtensions:@[AEPMobileSignal.class, AEPMobileLifecycle.class, AEPMobileUserProfile.class, AEPMobileIdentity.class, AEPMobileAssurance.class] completion:^{
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
import AEPAssurance
import AEPCore
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPUserProfile

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([Signal.self, Lifecycle.self, UserProfile.self, Identity.self, Assurance.self], {
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
| [Identity](../foundation-extensions/mobile-core/identity/) | [AEPIdentity](../foundation-extensions/mobile-core/identity/migration.md) |
| [Lifecycle](../foundation-extensions/mobile-core/lifecycle/) | [AEPLifecycle](../foundation-extensions/mobile-core/lifecycle/acplifecycle-aeplifecycle.md) |
| [Signal](../foundation-extensions/mobile-core/signals/) | [AEPSignal](../foundation-extensions/mobile-core/signals/acpsignal-aepsignal.md) |
| [Profile](../foundation-extensions/profile/) | [AEPUserProfile](../foundation-extensions/profile/acpuserprofile-aepuserprofile.md) |
| [Adobe Experience Platform Assurance](../foundation-extensions/adobe-experience-platform-assurance/) | [AEPAssurance](../foundation-extensions/adobe-experience-platform-assurance/migration.md) |
| [Adobe Experience Platform Places Service](../foundation-extensions/places/) | [AEPPlaces](../foundation-extensions/places/migration.md) |
| [Adobe Analytics - Mobile Services](../using-mobile-extensions/adobe-analytics-mobile-services/) | [AEPMobileService](../using-mobile-extensions/adobe-analytics-mobile-services/migration.md) |
| [Adobe Analytics](../using-mobile-extensions/adobe-analytics/) | [AEPAnalytics](../using-mobile-extensions/adobe-analytics/migration.md) |
| [Adobe Analytics - Media Analytics for Audio & Video](../using-mobile-extensions/adobe-media-analytics/) | [AEPMedia](../using-mobile-extensions/adobe-media-analytics/migration.md) |
| [Adobe Audience](../using-mobile-extensions/adobe-audience-manager/) | [AEPAudience](../using-mobile-extensions/adobe-audience-manager/migration.md) |
| [Adobe Experience Platform Target](../using-mobile-extensions/adobe-target/) | [AEPTarget](../using-mobile-extensions/adobe-target/migration.md) |
| [Adobe Experience Platform Campaign](../using-mobile-extensions/adobe-campaign-standard/) | [AEPCampaign](../using-mobile-extensions/adobe-campaign-standard/migration.md) |

