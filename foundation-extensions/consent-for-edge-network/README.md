# Consent for Edge Network

The Adobe Experience Platform Consent mobile extension enables consent preferences collection from your mobile app when using the [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/mobile-core) and the [Edge Network extension](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge).

## Configure the Adobe Experience Platform Consent extension in Experience Platform Launch

1. In Experience Platform Launch, in your mobile property, click the **Extensions** tab.
2. On the **Catalog** tab, locate or search for the **Consent** extension, and click **Install**.
3. Set your desired default consent level.
4. Click **Save**.
5. Follow the publishing process to update SDK configuration.

![AEP Consent extension configuration](../../.gitbook/assets/mobile-edge-consent-launch-configuration.png)

## Add the AEP Consent extension to your app

### Download and import the Consent extension

{% tabs %}
{% tab title="Android" %}
### Java

1. Add the Mobile Core and Edge extensions to your project using the app's Gradle file.

   ```java
   implementation 'com.adobe.marketing.mobile:core:1.+'
   implementation 'com.adobe.marketing.mobile:edge:1.+'
   implementation 'com.adobe.marketing.mobile:edgeidentity:1.+'
   implementation 'com.adobe.marketing.mobile:edgeconsent:1.+'
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
```

### Objective-C

```text
// AppDelegate.h
@import AEPCore;
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPEdgeConsent;
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
        Consent.registerExtension(); // register Consent
        Identity.registerExtension();
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
    MobileCore.registerExtensions([Identity.self, Edge.self, Consent.self], {
        MobileCore.configureWith(appId: "yourLaunchEnvironmentID")
    })
  ...
}
```

### Objective-C

```text
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileEdgeIdentity.class, AEPMobileEdge.class, AEPMobileEdgeConsent.class] completion:^{
    [AEPMobileCore configureWithAppId: @"yourLaunchEnvironmentID"];
  }];
  ...
}
```
{% endtab %}
{% endtabs %}

## Configuration keys

To update the SDK configuration programmatically, use the following information to change the Edge Consent configuration values.

| Key | Required | Description | Data Type |
| :--- | :--- | :--- | :--- |
| consent.default | No | Consents in XDM format. For more details, see [Privacy/Personalization/Marketing Preferences (Consents) Schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-consents.schema.md). | Map |

