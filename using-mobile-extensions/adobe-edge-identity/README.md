# Adobe Experience Platform Identity
The Adobe Experience Platform Identity mobile extension enables identity management from your mobile app when using the [Adobe Experience Platform](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/mobile-core) and the [Edge Network extension](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge).

## Add the AEP Identity extension to your app

### Download and import the Identity extension
{% hint style="info" %}
The following instructions are for configuring an application using Adobe Experience Platform Edge mobile extensions. If an application will include both Edge Network and Adobe Solution extensions, both the Identity for Edge Network and Identity for Experience Cloud ID Service extensions are required. Find more details in the [Frequently Asked Questions](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-identity/edge-identity-faq#download-and-import-the-identity-and-identity-for-edge-network-extensions) page.
{% endhint %}

{% tab title="Android" %}
### Java

1. Add the Mobile Core and Edge extensions to your project using the app's Gradle file.

   ```java
   implementation 'com.adobe.marketing.mobile:core:1.+'
   implementation 'com.adobe.marketing.mobile:edge:1.+'
   implementation 'com.adobe.marketing.mobile:edgeidentity:1.+'
   ```
   
2. Import the Mobile Core and Edge extensions in your application class.

   ```java
    import com.adobe.marketing.mobile.*;
   ```
{% endtab %}

{% tab title="iOS" %}
1. Add the Mobile Core and Edge extensions to your project using CocoaPods. Add following pods in your `Podfile`:

   ```swift
   use_frameworks!
   target 'YourTargetApp' do
       pod 'AEPCore'
       pod 'AEPEdge'
       pod 'AEPEdgeIdentity'
   end
   ```
   
2. Import the Mobile Core and Edge libraries:

### Swift

```swift
// AppDelegate.swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
```

### Objective-C

```objectivec
// AppDelegate.h
@import AEPCore;
@import AEPEdge;
@import AEPEdgeIdentity;
```
{% endtab %}
{% endtabs %}

### Register the Identity extension with Mobile Core

{% tabs %}
{% tab title="Android" %}

### Java

```java
public class MobileApp extends Application {

    @Override
    public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);
      MobileCore.configureWithAppID("yourLaunchEnvironmentID");

      Edge.registerExtension();
      Identity.registerExtension();
      MobileCore.start(new AdobeCallback() {
        @Override
        public void call(final Object o) {
          // processing after start
        }});
    }
}
```
{% endtab %}

{% tab title="iOS" %}
### Swift

```swift
// AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([Identity.self, Edge.self], {
    MobileCore.configureWith(appId: "yourLaunchEnvironmentID")
  })
  ...
}
```

### Objective-C

```objectivec
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileEdgeIdentity.class, AEPMobileEdge.class] completion:^{
    ...
  }];
  [AEPMobileCore configureWithAppId: @"yourLaunchEnvironmentID"];
  ...
}
```
{% endtab %}
{% endtabs %}

## What OS & platform versions are supported?

* Android versions 4.4 or later \(API levels 19 or later\)
* iOS versions 10 or later


