# Frequently Asked Questions

## Q: I am using AEP Edge and Adobe Solutions extensions, which Identity Extension should I install and register?
### A: Both. 
When using both Adobe Experience Platform Edge and Adobe Solutions extensions, both Edge Identity and Identity direct extensions can be registered with the Mobile SDK at the same time. 

### Download and import the Identity and Edge Identity extensions
{% hint style="info" %}

The following instructions are for configuring an application using both Edge Network and Adobe Solutions mobile extensions. If an application will include only Adobe Experience Platform Edge extensions, follow the instructions [here](./README#download-and-import-the-edge-identity-extension).
{% tabs %}

{% tabs %}
{% tab title="Android" %}
### Java

1. Add the Mobile Core and Edge extensions to your project using the app's Gradle file.

   ```java
   implementation 'com.adobe.marketing.mobile:core:1.+'
   implementation 'com.adobe.marketing.mobile:identity:1.+'
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
       pod 'AEPIdentity'
       pod 'AEPEdge'
       pod 'AEPEdgeIdentity'
   end
   ```
   
2. Import the Mobile Core and Edge libraries:

### Swift

```swift
// AppDelegate.swift
import AEPCore
import AEPIdentity
import AEPEdge
import AEPEdgeIdentity
```

### Objective-C

```objectivec
// AppDelegate.h
@import AEPCore;
@import AEPIdentity;
@import AEPEdge;
@import AEPEdgeIdentity;
```
{% endtab %}
{% endtabs %}

### Register the Identity and Edge Identity extensions with Mobile Core

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

      try {
        Edge.registerExtension();
        com.adobe.marketing.mobile.edge.identity.Identity.registerExtension(); // Register Edge Identity with Mobile Core
        com.adobe.marketing.mobile.Identity.registerExtension(); // Register Identity with Mobile Core
        MobileCore.start(new AdobeCallback() {
          @Override
          public void call(final Object o) {
            // processing after start
          }});
      } catch (Exception e) {
         //Log the exception
     }
    }
}
```
{% endtab %}

{% tab title="iOS" %}
### Swift

```swift
// AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([AEPEdgeIdentity.Identity.self, AEPIdentity.Identity.self, Edge.self], {
    MobileCore.configureWith(appId: "yourLaunchEnvironmentID")
  })
  ...
}
```

### Objective-C

```objectivec
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileEdgeIdentity.class, AEPMobileIdentity.class, AEPMobileEdge.class] completion:^{
    ...
  }];
  [AEPMobileCore configureWithAppId: @"yourLaunchEnvironmentID"];
  ...
}
```
{% endtab %}
{% endtabs %}