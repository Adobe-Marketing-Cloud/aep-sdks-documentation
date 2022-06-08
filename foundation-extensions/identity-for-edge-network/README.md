# Identity for Edge Network

The Adobe Experience Platform Identity mobile extension enables identity management from your mobile app when using the Adobe Experience Platform Mobile SDK and the [Edge Network extension](../experience-platform-extension/).

## Configure the Adobe Experience Platform Identity extension in the Data Collection UI

1. In Data Collection UI, in your mobile property, select the **Extensions** tab.
2. On the **Catalog** tab, locate or search for the **Identity** extension, and select **Install**.
3. There are no configuration settings for **Identity**.
4. Select **Save**.
5. Follow the publishing process to update SDK configuration.

![AEP Identity for Edge Network extension configuration](../../.gitbook/assets/mobile-edge-identity-launch-configuration.png)

## Add the AEP Identity extension to your app

### Download and import the Identity extension

{% hint style="info" %}
The following instructions are for configuring an application using Adobe Experience Platform Edge mobile extensions. If an application will include both Edge Network and Adobe Solution extensions, both the Identity for Edge Network and Identity for Experience Cloud ID Service extensions are required. Find more details in the [frequently asked questions](identity-faq.md).
{% endhint %}

{% hint style="info" %}
When using the [`setAdvertisingIdentifier`](./api-reference.md#setadvertisingidentifier) API, see the setup guide for [AEP Consent for Edge Network](../consent-for-edge-network/README.md) for instructions on setting up the extension and profile schema for proper usage.
{% endhint %}

{% tabs %}
{% tab title="Android" %}

1. Add the Mobile Core and Edge extensions to your project using the app's Gradle file.

   ```java
   implementation 'com.adobe.marketing.mobile:core:1.+'
   implementation 'com.adobe.marketing.mobile:edge:1.+'
   implementation 'com.adobe.marketing.mobile:edgeidentity:1.+'
   implementation 'com.adobe.marketing.mobile:edgeconsent:1.+' // Recommended when using the setAdvertisingIdentifier API
   ```

2. Import the Mobile Core and Edge extensions in your Application class.

### Java

```java
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.edge.identity.Identity;
import com.adobe.marketing.mobile.edge.consent.Consent;
```

### Kotlin

```kotlin
import com.adobe.marketing.mobile.MobileCore
import com.adobe.marketing.mobile.Edge
import com.adobe.marketing.mobile.edge.identity.Identity
import com.adobe.marketing.mobile.edge.consent.Consent
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
       pod 'AEPEdgeConsent' // Recommended when using the setAdvertisingIdentifier API
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

```objectivec
// AppDelegate.h
@import AEPCore;
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPEdgeConsent;
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

This extension is built on the AEPCore (3.x) and it is not compatible with ACPCore (2.x). Please follow [the guide for migrating to the Swift AEPCore](../../resources/migrate-to-swift.md).

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
      try {
        Edge.registerExtension();
        Identity.registerExtension();
        Consent.registerExtension();
        // Register other extensions here
        MobileCore.start(new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID("yourAppId");
            }
        });      

      } catch (Exception e) {
        ...
      }


    }
}
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

```swift
// AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([Identity.self, Consent.self, Edge.self], {
    MobileCore.configureWith(appId: "yourLaunchEnvironmentID")
  })
  ...
}
```

### Objective-C

```objectivec
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileEdgeIdentity.class, AEPMobileEdgeConsent.class, AEPMobileEdge.class] completion:^{
    ...
  }];
  [AEPMobileCore configureWithAppId: @"yourLaunchEnvironmentID"];
  ...
}
```
{% endtab %}
{% endtabs %}

## Advertising Identifier
The Edge Identity extension compares the previously stored advertising identifier value with the new value received from the `setAdvertisingIdentifier` API and handles the following scenarios:

Ad tracking enabled - when the new value sent to the API is:
- A valid UUID string (example: `"a127a99e-50be-4d87-bf6f-6ab9541c105b"`)

Process:
1. Updates the client side XDM `IdentityMap` with the new value for IDFA/GAID, and it will be sent with any future [XDM Experience events](../experience-platform-extension/xdm-experience-events.md). For more details on these namespaces see the [standard Identity namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#standard). 
2. Sends a [consent update event](https://experienceleague.adobe.com/docs/experience-platform/xdm/data-types/consents.html) with ad ID consent preferences set to `yes` (only when a valid ad ID is absent from the `IdentityMap` and the Edge Consent extension is registered and properly configured).

Ad tracking disabled - Given a valid ad ID already exists in the `IdentityMap`, and the new value  sent to the API is: 
- `null`/`nil`
- Empty string (`""`)
- All-zeros string (`"00000000-0000-0000-0000-000000000000"`)  

Process:
1. Removes the ad ID from the client side XDM `IdentityMap`, and it will not be sent with any future [XDM Experience events](../experience-platform-extension/xdm-experience-events.md).
2. Sends a [consent update event](https://experienceleague.adobe.com/docs/experience-platform/xdm/data-types/consents.html) with ad ID consent preferences set to `no` (only when the Edge Consent extension is registered and properly configured).

No operations are executed when no changes are detected between the previously stored and new ad ID value.