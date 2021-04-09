# Frequently Asked Questions

## Q: I am using AEP Edge and Adobe Solutions extensions, which Identity Extension should I install and register?
### A: Both. 
When using both Adobe Experience Platform Edge and Adobe Solutions extensions, both Edge Identity and Identity direct extensions can be registered with the Mobile SDK at the same time. 

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


## Q: Will an existing Experience Cloud ID (ECID) migrate to the AEP Edge Identity extension?
### A: Yes
If the application previously installed the AEP Identity direct solution extension and upgrades to the AEP Edge Identity extension, the existing ECID value is migrated to the AEP Edge Identity extension on first launch of the application.

Note, however, if the Mobile SDK's privacy status was set to `optedOut` at the time the application is upgraded, the AEP Identity direct solution extension will not have an ECID, as it was cleared. In this case, the AEP Edge Identity extension will generate a new ECID.


## Q: What is the Experience Cloud ID (ECID) used by the SDK when using both AEP Edge extensions and Adobe Solutions extensions?
### A: The AEP Edge Identity extension and the AEP Identity direct solution extension each manage their own ECID.

At first launch of the application after upgrading to the AEP Edge Identity extension, the existing ECID from the AEP Identity direct solution extension is migrated to the AEP Edge Identity extension. In this case both extensions will have the same ECID value.

The [resetIdentities](./edge-identity-api-reference#resetIdentities) API regenerates a new ECID used by the AEP Edge Identity extension. This API call does not change the ECID used by the AEP Identity direct solution extension. After calling this API, the ECID used by each identity extension will be different.

Changing the privacy status to `optedOut` will clear the ECID value used by the AEP Identity direct solution extension. Changing the privacy status back to `optedIn` will generate a new ECID used by the AEP Identity direct solution extension. Privacy status changes do not change the ECID used by the AEP Edge Identity extension. Changing the privacy status will cause the ECID used by each identity extension to be different.

When each identity extension has a different ECID, the AEP Edge Identity extension will include the AEP Identity direct solution ECID in its [IdentityMap](./edge-identity-api-reference#identitymap) by listening to state changes from the AEP Identity direct solution extension. By including both ECIDs in the `IdentityMap`, the Adobe Experience Platform Identity Service will link the two ECIDs in the customer's Identity Graph.

The following example shows an IdentityMap containing the ECIDs from both AEP Edge Identity extension and AEP Identity direct solution extension. The ECID from the AEP Edge Identity extension is always listed first in the list of ECIDs.
```json
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
### A: The AEP Edge Identity does not change its ECID based on privacy status changes.

{% hint style="info" %}
The AEP Edge Identity extension and the AEP Identity direct solution extension each manage their own ECID value and are generated independently of each other. 
{% endhint %}

The AEP Edge Identity extension does not clear its stored identities or regenerate the ECID due to privacy status changes. Instead, use the [resetIdentities](./edge-identity-api-reference#resetidentities) API. Note this API does not clear the ECID but instead generates a new ECID.

Each identity extension has its own API to retrieve their respective ECIDs as well. Use [Identity.getExperienceCloudId](./edge-identity-api-reference#getexperiencecloudid) to get the AEP Edge Identity ECID, and [Identity.getExperienceCloudId](../mobile-core/identity/identity-api-reference#getexperiencecloudid) to get the AEP Identity direct solution ECID.


## Q: How can I get all the identifiers used by the SDK when using both AEP Edge extensions and Adobe Solutions extensions?
### A: Use both [getSdkIdentities](../mobile-core/mobile-core-api-reference#retrieving-stored-identifiers) and [getIdentities](./edge-identity-api-reference#getidentities)

To get the identifiers used by the Adobe Solutions extensions, call [getSdkIdentities](../mobile-core/mobile-core-api-reference#retrieving-stored-identifiers).

To get the identifiers used by the AEP Edge extensions, call [getIdentities](./edge-identity-api-reference#getidentities).


## Q: How can I clear all the identifiers from the SDK when using both AEP Edge extensions and Adobe Solutions extensions?
### A: Set privacy status to `optedOut` and call `resetIdentities`

To clear the identifiers used by the Adobe Solutions extensions, call [setPrivacyStatus](../resources/privacy-and-gdpr#setprivacystatus) and set the privacy status to `optedOut`.

To clear the identifiers used by the AEP Edge extensions, call [resetIdentities](../mobile-core/mobile-core-api-reference#reset-identities)


## Q: What steps are needed to generate a new Experience Cloud ID (ECID) for a user when using both AEP Edge extensions and Adobe Solutions extensions?
### A: Both identity extensions' ECID must be regenerated in sequence to avoid linking the old and new ECIDs in Adobe Experience Platform.

When using Real-time Customer Profile and Identity Service, the ECIDs from both identity extensions are linked together in the customer's Identity Graph. Care must be taken when regenerating new ECIDs such that the old and new ECIDs are not linked within the same Identity Graph.

Perform the following API calls to regenerate the ECIDs in sequence:
1. Set [privacy status](../resources/privacy-and-gdpr#setprivacystatus) to `optedOut` to clear the ECID from the AEP Identity direct service extension.
2. Call [resetIdentities](./edge-identity-api-reference#resetidentities) to regenerate a new ECID in the AEP Edge Identity extension.
3. Call [getExperienceCloudId](./edge-identity-api-reference#getexperiencecloudid) on the AEP Edge Identity extension. This ensures the new ECID is generated before continuing.
4. Set [privacy status](../resources/privacy-and-gdpr#setprivacystatus) to `optedIn` to generate a new ECID in the AEP Identity direct service extension.

After completing the above steps, each identity extension will have its own, different, ECID. The new ECIDs will get linked under a new Identity Graph for the customer.


## Q: I would like to enable my XDM schema for Profile. Which identifier should be marked as primary?
### A: Only one identity in the IdentityMap may be marked primary.

{% hint style="info" %}
There can be only one primary identity per request event and the primary identity must be contained within the [IdentityMap](./edge-identity-api-reference#identitymap).
{% endhint %}

By default, the ECID from the AEP Edge Identity extension is the primary identifier for the Experience Event request. Once an Experience Event is received by the AEP Edge Network, if no identity is primary, it will mark the ECID as primary.

To set a different identifier as primary for an Experience Event, use the [updateIdentities](./edge-identity-api-reference#updateidentities) API.

{% tabs %}
{% tab title="Android" %}

### Java

```java
IdentityItem item = new IdentityItem("user@example.com", AuthenticatedState.AUTHENTICATED, true);
IdentityMap identityMap = new IdentityMap();
identityMap.addItem(item, "Email")
Identity.updateIdentities(identityMap);
```
{% endtab %}

{% tab title="iOS" %}
### Swift

```swift
let item = IdentityItem(id: "user@example.com", authenticatedState: .authenticated, primary: true)
let identityMap = IdentityMap()
map.addItem(item: item , withNamespace: "Email")
Identity.updateIdentities(with: identityMap)
```

### Objective-C

```objectivec
AEPIdentityItem *item = [[AEPIdentityItem alloc] initWithId:@"user@example.com" authenticatedState:AEPAuthenticatedStateAuthenticated primary:true];
AEPIdentityMap *map = [[AEPIdentityMap alloc] init];
[map addItem:item withNamespace:@"Email"];
[AEPMobileEdgeIdentity updateIdentities:map];
```
{% endtab %}
{% endtabs %}


## Q: I use multiple XDM schemas enabled for Profile, can I use different primary identifiers for each?
### A: Yes

The [IdentityMap](./edge-identity-api-reference#identitymap) in the AEP Edge Identity extension is automatically included on each call to [Edge.sendEvent](../edge/edge-api-reference#sendevent). When using multiple Experience Data Model (XDM) schemas where each uses a different primary identifier, you will need to pass the primary identifier with each request, instead of marking a primary identifier in the AEP Edge Identity `IdentityMap`.

{% tabs %}
{% tab title="Android" %}
### Java

```java

```
{% endtab %}

{% tab title="iOS" %}
### Swift

```swift
let item = IdentityItem(id: "user@example.com", authenticatedState: .authenticated, primary: true)
let identityMap = IdentityMap()
identityMap.add(item: item, withNamespace: "Email")

// Sample example using the Commerce schema
var xdmData: [String: Any] = [
    "commerce": [
        "productListViews": [
            "value": 1
        ]
    ],
    "productListItems": [
        [
            "SKU": "1002352692",
            "product": "https://commerce.adobe.io/entities/product/product-203766910"
        ]
    ]
]

// Encode the IdentityMap to a dictionary and add to the XDM data dictionary
if let dict = identityMap.asDictionary() {
    xdmData["identityMap"] = dict
}

let experienceEvent = ExperienceEvent(xdm: xdmData, datasetIdentifier: "1234567890")
Edge.sendEvent(experienceEvent: experienceEvent)
```

### Objective-C

```objectivec

```
{% endtab %}
{% endtabs %}
