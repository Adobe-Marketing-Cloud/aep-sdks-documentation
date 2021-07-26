# Frequently asked questions

## Q: I am using AEP Edge and Adobe Solutions extensions, which Identity Extension should I install and register?

### A: Both.

When using both Adobe Experience Platform Edge and Adobe Solutions extensions, both Identity for Edge Network and Identity for Experience Cloud ID Service extensions can be registered with the Mobile SDK at the same time.

{% hint style="info" %}
The following instructions are for configuring an application using both Edge Network and Adobe Solutions mobile extensions. If an application will include only Adobe Experience Platform Edge extensions, follow the instructions [here](./#download-and-import-the-identity-extension).
{% endhint %}

#### Download and import the Identity and Identity for Edge Network extensions

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

#### Register the Identity and Identity for Edge Network extensions with Mobile Core

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
        com.adobe.marketing.mobile.edge.identity.Identity.registerExtension(); // Register Identity for Edge Network with Mobile Core
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

## Q: Will an existing Experience Cloud ID \(ECID\) migrate to the Identity for Edge Network extension?

### A: Yes

If the application previously installed the Identity for Experience Cloud ID Service extension and upgrades to the Identity for Edge Network extension, the existing ECID value is migrated to the Identity for Edge Network extension on first launch of the application.

Note, however, if the Mobile SDK's privacy status was set to `optedOut` at the time the application is upgraded, the Identity for Experience Cloud ID Service extension will not have an ECID, as it was cleared. In this case, the Identity for Edge Network extension will generate a new ECID.

## Q: What is the Experience Cloud ID \(ECID\) used by the SDK when using both AEP Edge extensions and Adobe Solutions extensions?

### A: The Identity for Edge Network extension and the Identity for Experience Cloud ID Service extension each manage their own ECID. However, the two ECIDs are synced as part of the XDM IdentityMap.

At first launch of the application after upgrading to the Identity for Edge Network extension, the existing ECID from the Identity for Experience Cloud ID Service extension is migrated to the Identity for Edge Network extension. In this case both extensions will have the same ECID value.

The [resetIdentities](api-reference.md#resetidentities) API regenerates a new ECID used by the Identity for Edge Network extension. This API call does not change the ECID used by the Identity for Experience Cloud ID Service extension. After calling this API, the ECID used by each identity extension will be different.

Changing the privacy status to `optedOut` will clear the ECID value used by the Identity for Experience Cloud ID Service extension. Changing the privacy status back to `optedIn` will generate a new ECID used by the Identity for Experience Cloud ID Service extension. Privacy status changes do not change the ECID used by the Identity for Edge Network extension. Changing the privacy status will cause the ECID used by each identity extension to be different.

When each identity extension has a different ECID, the Identity for Edge Network extension will include the Identity for Experience Cloud ID Service ECID in its [IdentityMap](api-reference.md#identitymap), and so the Adobe Experience Platform Identity Service will link the the two ECIDs in the customer's Identity Graph.

The following example shows an IdentityMap containing the ECIDs from both Identity for Edge Network extension and Identity for Experience Cloud ID Service extension. The ECID from the Identity for Edge Network extension is always listed first in the list of ECIDs.

```javascript
"identityMap" : {
      "ECID" : [
        {
          "id" : "73586628797489658169123381027155647197",
          "authenticatedState" : "ambiguous",
          "primary" : false
        },
        {
          "id" : "81117527655405132265917409409236407340",
          "authenticatedState" : "ambiguous",
          "primary" : false
        }
      ]
    }
```

## Q: I set privacy status to opted out, why do I see an ECID value when calling `Identity.getExperienceCloudId()`?

### A: The Identity for Edge Network extension does not change its ECID based on privacy status changes.

{% hint style="info" %}
The Identity for Edge Network extension and the Identity for Experience Cloud ID Service extension each manage their own ECID value and are generated independently of each other.
{% endhint %}

The Identity for Edge Network extension does not clear its stored identities or regenerate the ECID due to privacy status changes. Instead, use the [resetIdentities](edge-identity-api-reference.md#resetidentities) API. Note this API does not clear the ECID but instead generates a new ECID.

Each identity extension has its own API to retrieve their respective ECIDs as well. Use [Identity.getExperienceCloudId](api-reference.md#getexperiencecloudid) to get the Identity for Edge Network extension's ECID, and [Identity.getExperienceCloudId](../mobile-core/identity/identity-api-reference.md#getexperiencecloudid) to get the Identity for Experience Cloud ID Service extension's ECID.

## Q: How can I get all the identifiers used by the SDK when using both AEP Edge extensions and Adobe Solutions extensions?

### A: Use both `getSdkIdentities` and `getIdentities`

To get the identifiers used by the Adobe Solutions extensions, call [getSdkIdentities](../mobile-core/mobile-core-api-reference.md#retrieving-stored-identifiers).

To get the identifiers used by the AEP Edge extensions, call [getIdentities](api-reference.md#getidentities).

## Q: How can I clear all the identifiers from the SDK when using both AEP Edge extensions and Adobe Solutions extensions?

### A: Set privacy status to `optedOut` and call `resetIdentities`

To clear the identifiers used by the Adobe Solutions extensions, call [setPrivacyStatus](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr#set-and-get-privacy-status) and set the privacy status to `optedOut`.

To clear the identifiers used by the AEP Edge extensions, call [resetIdentities](../mobile-core/mobile-core-api-reference.md#reset-identities)

## Q: What steps are needed to generate a new Experience Cloud ID \(ECID\) for a user when using both AEP Edge extensions and Adobe Solutions extensions?

### A: Both identity extensions' ECID must be regenerated in sequence to avoid linking the old and new ECIDs in Adobe Experience Platform.

When using Real-time Customer Profile and Identity Service, the ECIDs from both identity extensions are linked together in the customer's Identity Graph. Care must be taken when regenerating new ECIDs such that the old and new ECIDs are not linked within the same Identity Graph.

Perform the following API calls to regenerate the ECIDs in sequence: 

1. Set [privacy status](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr#set-and-get-privacy-status) to `optedOut` to clear the ECID from the AEP Identity direct service extension. 
2. Call [resetIdentities](api-reference.md#resetidentities) to regenerate a new ECID in the Identity for Edge Network extension. 
3. Call [getExperienceCloudId](api-reference.md#getexperiencecloudid) on the Identity for Edge Network extension. This ensures the new ECID is generated before continuing. 
4. Set [privacy status](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr#set-and-get-privacy-status) to `optedIn` to generate a new ECID in the AEP Identity direct service extension.

After completing the above steps, each identity extension will have its own, different, ECID. The new ECIDs will get linked under a new Identity Graph for the customer.

{% tabs %}
{% tab title="Android" %}
### Java

```java
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT);
MobileCore.resetIdentities();
com.adobe.marketing.mobile.edge.identity.Identity.getExperienceCloudId(new AdobeCallback<String>() {
    @Override
    public void call(String s) {
        // ignore
    }
});
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN);
```
{% endtab %}

{% tab title="iOS" %}
### Swift

```swift
MobileCore.setPrivacyStatus(.optedOut)
MobileCore.resetIdentities()
AEPEdgeIdentity.Identity.getExperienceCloudId { _, _ in }
MobileCore.setPrivacyStatus(.optedIn)
```

### Objective-C

```objectivec
[AEPMobileCore setPrivacyStatus:AEPPrivacyStatusOptedOut];
[AEPMobileCore resetIdentities];
[AEPMobileEdgeIdentity getExperienceCloudId:^(NSString *ecid, NSError *error) {
    // ignore
}];
[AEPMobileCore setPrivacyStatus:AEPPrivacyStatusOptedIn];
```
{% endtab %}
{% endtabs %}

