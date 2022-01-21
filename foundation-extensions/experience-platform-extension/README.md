# Adobe Experience Platform Edge Network

## Before starting

### Install Identity for Edge Network

The Adobe Experience Platform Edge Network extension requires the Identity for Edge Network extension in order to operate. As a first step install and configure the [Identity for Edge Network](../identity-for-edge-network) extension, then continue with the steps below.



## Configure the Edge Network extension in Platform

1. In Experience Platform, in your mobile property, click the **Extensions** tab.
2. On the **Catalog** tab, locate or search for the **Adobe Experience Platform Edge Network** extension, and click **Install**.
3. Type in the extension settings. For more information, see [Configure datastreams](../../getting-started/configure-datastreams.md) and [datastreams](./#datastreams).
4. Click **Save**.
5. Follow the publishing process to update SDK configuration.

![Edge Network extension configuration](../../.gitbook/assets/mobile-edge-launch-configuration.png)

### Datastreams

Select the `Datastream` from the drop-down list. Once you do that, the Production, Staging and Development Environments will be automatically prefilled. If no Datastream was previously created, see [Configure datastreams](../../getting-started/configure-datastreams.md).

If you use multiple Development configurations, select the desired one from the `Development Environment` drop-down.

The Datastream used by the client-side implementation is one of the followings:

* the `Production Environment` configuration when the Launch library is published to production \(in the Published column in the Launch publishing flow\).
* the`Staging Environment` configuration when the Launch library is published to staging \(in the Submitted column in the Launch publishing flow\).
* the `Development Environment` configuration when the Launch library is in development.

### Edge Network domain

If you have a first-party domain mapped to the Adobe-provisioned Edge Network domain, enter it here. The domain name is expected to be just the domain without any protocol or trailing slash. To use the default Adobe Edge Network domain, leave this field blank.

Entering an Edge Network domain will add an `edge.domain` key in the mobile property. 

## Add the Edge Network extension to your app

### Download and import the Edge extension

{% tabs %}
{% tab title="Android" %}
#### Java

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

{% tab title="iOS (AEP 3.x)" %}

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

#### Swift

```swift
// AppDelegate.swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
```

#### Objective-C

```objective-c
// AppDelegate.h
@import AEPCore;
@import AEPEdge;
@import AEPEdgeIdentity;
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

This extension is built on the AEPCore (3.x) and it is not compatible with ACPCore (2.x). Please follow [the guide for migrating to the Swift AEPCore](https://aep-sdks.gitbook.io/docs/resources/migrate-to-swift).

{% endtab %}

{% endtabs %}

### Register Edge with Mobile Core

{% tabs %}
{% tab title="Android" %}

#### Java

```java
public class MobileApp extends Application {

    @Override
    public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);
      MobileCore.configureWithAppID("yourAppId");

      try {
        Edge.registerExtension();
        com.adobe.marketing.mobile.edge.identity.Identity.registerExtension();
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

{% tab title="iOS (AEP 3.x)" %}
#### Swift

```swift
// AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([Edge.self, AEPEdgeIdentity.Identity.self], {
    MobileCore.configureWith(appId: "yourAppId")
  })
  ...
}
```

#### Objective-C

```objective-c
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileEdge.class, AEPMobileEdgeIdentity.class] completion:^{
    ...
  }];
  [AEPMobileCore configureWithAppId: @"yourAppId"];
  ...
}
```
{% endtab %}

{% endtabs %}

## Next steps

Install other extensions based on your use-case:

1. If your application requires user consent preferences collection and enforcement, install and configure the [Consent for Edge Network](../consent-for-edge-network) extension.
2. Lifecycle extension now supports application lifecycle metrics collection for Edge Network. If you would like to start collecting this type of data, follow the installation instruction for [Lifecycle for Edge Network](../lifecycle-for-edge-network).
3. If your application uses push notifications, see also the [Adobe Journey Optimizer](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer) extension.

## Configuration keys

To update the SDK configuration programmatically, use the following information to change the Edge configuration values.

| Key | Required | Description | Data Type |
| :--- | :--- | :--- | :--- |
| edge.configId | Yes | See [datastreams](./#datastreams). | String |
| edge.domain   | No  | A custom first-party domain mapped to the Adobe provisioned Edge Network domain. | String |

