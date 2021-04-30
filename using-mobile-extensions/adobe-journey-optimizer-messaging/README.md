# Adobe Journey Optimizer Messaging

The Adobe Journey Optimizer Messaging mobile extension extension allows configuring and receiving push messages from your mobile app based on Adobe Experience Platform and Journey Orchestration.

## Prerequisites

* IMS organization is enabled for messaging.
* [Mobile Core](../mobile-core/README.md) and [Adobe Experience Platform Edge Network](../adobe-edge/README.md) extensions have been implemented in the app. 
Make sure that the [Edge Configuration](../adobe-edge/README.md#edge-configuration) used in the Edge extension has a Profile Dataset selected. For more information, see [Set up the Edge Configuration](../../getting-started/edge-configuration.md)

## Configure the Adobe Journey Optimizer Messaging extension in Experience Platform Launch

1. In Experience Platform Launch, in your mobile property, click the **Extensions** tab.
2. On the **Catalog** tab, locate or search for the **Adobe Journey Optimizer - Messaging** extension, and click **Install**.
3. Select the **Event Dataset** for Production, Stage and Development Environments. The datasets selected should use a schema that uses the Push Notification Tracking mixin. For more information, see [Setup Schemas & Datasets](../../getting-started/configure-schema-and-dataset.md).
4. Click **Save**.
5. Follow the publishing process to update SDK configuration.

![AEP Messaging extension configuration](../../.gitbook/assets/mobile-edge-consent-launch-configuration.png)

## Add the AOJ Messaging extension to your app

### Download and import the Messaging extension

{% tabs %}
{% tab title="Android" %}

### Java

1. Add the Mobile Core and Edge extensions to your project using the app's Gradle file.

   ```java
   implementation 'com.adobe.marketing.mobile:core:1.+'
   implementation 'com.adobe.marketing.mobile:edge:1.+'
   implementation 'com.adobe.marketing.mobile:edgeidentity:1.+'
   implementation 'com.adobe.marketing.mobile:messaging:1.+'
   ```
   
2. Import the Mobile Core and Edge extensions in your application class.

   ```java
    import com.adobe.marketing.mobile.*;
   ```


{% endtab %}

{% tab title="iOS" %}

1. Add the Mobile Core and Edge extensions to your project using Cocoapods. Add following pods in your `Podfile`:

   ```swift
   use_frameworks!
   target 'YourTargetApp' do
       pod 'AEPCore'
       pod 'AEPEdge'
       pod 'AEPEdgeIdentity'
       pod 'AEPMessaging'
   end
   ```
   
2. Import the Mobile Core and Edge libraries:

### Swift

```swift
// AppDelegate.swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPMessaging
```

### Objective-C

```text
// AppDelegate.h
@import AEPCore;
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPMessaging;
```

{% endtab %}
{% endtabs %}

### Register Edge extensions with Mobile Core

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
        Identity.registerExtension();
        AEPMessaging.registerExtension(); // register Messaging
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
    MobileCore.registerExtensions([Identity.self, Edge.self, AEPMessaging.self], {
    	MobileCore.configureWith(appId: "yourLaunchEnvironmentID")
    })
  ...
}
```

### Objective-C

```objective-c
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileEdgeIdentity.class, AEPMobileEdge.class, AEPMessaging.class] completion:^{
    [AEPMobileCore configureWithAppId: @"yourLaunchEnvironmentID"];
  }];
  ...
}
```

{% endtab %}
{% endtabs %}

## Configuration keys


## What OS & platform versions are supported?


