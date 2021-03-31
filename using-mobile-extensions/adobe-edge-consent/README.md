# Adobe Experience Platform Edge Consent

## Configure the Adobe Experience Platform Edge Consent extension in Experience Platform Launch

1. In Experience Platform Launch, in your mobile property, click the **Extensions** tab.
2. On the **Catalog** tab, locate or search for the **Consent Collection** extension, and click **Install**.
3. Set your desired default consent level.
4. Click **Save**.
5. Follow the publishing process to update SDK configuration.

### Configure the AEP Edge Consent extension

![Adobe Edge Network extension configuration](/Users/nporter/Developer/Documentation/acp-sdks-documentation/.gitbook/assets/mobile-edge-consent-launch-configuration.png)



## Add the AEP Edge Consent extension to your app

### Download and import the Edge Consent extension

{% tabs %}
{% tab title="Android" %}

### Java

1. Add the Mobile Core and Edge extensions to your project using the app's Gradle file.

   ```java
   implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
   implementation 'com.adobe.marketing.mobile:edge:1.+'
     implementation 'com.adobe.marketing.mobile.edgeidentity:1.+'
   implementation 'com.adobe.marketing.mobile.edgeconsent:1.+'
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
       pod 'AEPLifecycle'
       pod 'AEPSignal'
       pod 'AEPEdge'
       pod 'AEPEdgeIdentity'
       pod 'AEPEdgeConsent'
   end
   ```

2. Import the Mobile Core and Edge libraries:

### Swift

```swift
// AppDelegate.swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPLifecycle
import AEPSignal
```

### Objective-C

```text
// AppDelegate.h
@import AEPCore;
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPEdgeConsent;
@import AEPLifecycle;
@import AEPSignal;
```

{% endtab %}
{% endtabs %}

### Register Edge with Mobile Core

{% tabs %}
{% tab title="Android" %}

### Java

```java
public class MobileApp extends Application {

    @Override
    public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);
      MobileCore.configureWithAppID("yourAppId");

      try {
        Edge.registerExtension();
        Consent.registerExtension(); // register Consent
        com.adobe.marketing.mobile.edge.identity.Identity.registerExtension();
        Lifecycle.registerExtension();
        Signal.registerExtension();
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
    MobileCore.registerExtensions([Lifecycle.self, Identity.self, Signal.self, Edge.self, Consent.self], {
    MobileCore.configureWith(appId: "yourAppId")
  })
  ...
}
```

### Objective-C

```text
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileEdgeIdentity.class, AEPMobileLifecycle.class, AEPMobileSignal.class, AEPMobileEdge.class, AEPMobileEdgeConsent.class] completion:^{
    ...
  }];
  [AEPMobileCore configureWithAppId: @"yourAppId"];
  ...
}
```

{% endtab %}
{% endtabs %}

## Configuration keys

To update the SDK configuration programmatically, use the following information to change the Edge Consent configuration values.

| Key             | Required | Description                                                  | Data Type |
| :-------------- | :------- | :----------------------------------------------------------- | :-------- |
| consent.default | No       | Consents in XDM format. [More info.](https://github.com/adobe/xdm/blob/fc0773107f29928e1dc4753f8f055836083ea53f/docs/reference/mixins/profile/profile-consents.schema.md) | String    |

## What OS & platform versions are supported?

* Android versions 4.4 or later \(API levels 19 or later\)
* iOS versions 10 or later