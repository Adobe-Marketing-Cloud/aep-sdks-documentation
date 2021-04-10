# Frequently Asked Questions

## Q: I am using AEP Edge and Adobe Solutions extensions, which Identity Extension should I install and register?
### A: Both. 
When using both Adobe Experience Platform Edge and Adobe Solutions extensions, both Identity for Edge Network and Identity direct extensions can be registered with the Mobile SDK at the same time. 

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

### Register the Identity and Identity for Edge Network extensions with Mobile Core

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


## Q: Will an existing Experience Cloud ID (ECID) migrate to the Identity for Edge Network extension?
### A: Yes
If the application previously installed the Identity for Experience Cloud ID Service extension and upgrades to the Identity for Edge Network extension, the existing ECID value is migrated to the Identity for Edge Network extension on first launch of the application.

Note, however, if the Mobile SDK's privacy status was set to `optedOut` at the time the application is upgraded, the Identity for Experience Cloud ID Service extension will not have an ECID, as it was cleared. In this case, the Identity for Edge Network extension will generate a new ECID.


## Q: What is the Experience Cloud ID (ECID) used by the SDK when using both AEP Edge extensions and Adobe Solutions extensions?
### A: The Identity for Edge Network extension and the Identity for Experience Cloud ID Service extension each manage their own ECID. However, the two ECIDs are synced as part of the XDM IdentityMap.

At first launch of the application after upgrading to the Identity for Edge Network extension, the existing ECID from the Identity for Experience Cloud ID Service extension is migrated to the Identity for Edge Network extension. In this case both extensions will have the same ECID value.

The [resetIdentities](./edge-identity-api-reference#resetIdentities) API regenerates a new ECID used by the Identity for Edge Network extension. This API call does not change the ECID used by the Identity for Experience Cloud ID Service extension. After calling this API, the ECID used by each identity extension will be different.

Changing the privacy status to `optedOut` will clear the ECID value used by the Identity for Experience Cloud ID Service extension. Changing the privacy status back to `optedIn` will generate a new ECID used by the Identity for Experience Cloud ID Service extension. Privacy status changes do not change the ECID used by the Identity for Edge Network extension. Changing the privacy status will cause the ECID used by each identity extension to be different.

When each identity extension has a different ECID, the Identity for Edge Network extension will include the Identity for Experience Cloud ID Service ECID in its [IdentityMap](./edge-identity-api-reference#identitymap) by listening to state changes from the Identity for Experience Cloud ID Service extension. By including both ECIDs in the `IdentityMap`, the Adobe Experience Platform Identity Service will link the two ECIDs in the customer's Identity Graph.

The following example shows an IdentityMap containing the ECIDs from both Identity for Edge Network extension and Identity for Experience Cloud ID Service extension. The ECID from the Identity for Edge Network extension is always listed first in the list of ECIDs.
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
### A: The Identity for Edge Network extension does not change its ECID based on privacy status changes.

{% hint style="info" %}
The Identity for Edge Network extension and the Identity for Experience Cloud ID Service extension each manage their own ECID value and are generated independently of each other. 
{% endhint %}

The Identity for Edge Network extension does not clear its stored identities or regenerate the ECID due to privacy status changes. Instead, use the [resetIdentities](./edge-identity-api-reference#resetidentities) API. Note this API does not clear the ECID but instead generates a new ECID.

Each identity extension has its own API to retrieve their respective ECIDs as well. Use [Identity.getExperienceCloudId](./edge-identity-api-reference#getexperiencecloudid) to get the Identity for Edge Network extension's ECID, and [Identity.getExperienceCloudId](../mobile-core/identity/identity-api-reference#getexperiencecloudid) to get the Identity for Experience Cloud ID Service extension's ECID.


## Q: How can I get all the identifiers used by the SDK when using both AEP Edge extensions and Adobe Solutions extensions?
### A: Use both [getSdkIdentities](../mobile-core/mobile-core-api-reference#retrieving-stored-identifiers) and [getIdentities](./edge-identity-api-reference#getidentities)

To get the identifiers used by the Adobe Solutions extensions, call [getSdkIdentities](../mobile-core/mobile-core-api-reference#retrieving-stored-identifiers).

To get the identifiers used by the AEP Edge extensions, call [getIdentities](./edge-identity-api-reference#getidentities).


## Q: How can I clear all the identifiers from the SDK when using both AEP Edge extensions and Adobe Solutions extensions?
### A: Set privacy status to `optedOut` and call `resetIdentities`

To clear the identifiers used by the Adobe Solutions extensions, call [setPrivacyStatus](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr#set-and-get-privacy-status) and set the privacy status to `optedOut`.

To clear the identifiers used by the AEP Edge extensions, call [resetIdentities](../mobile-core/mobile-core-api-reference#reset-identities)


## Q: What steps are needed to generate a new Experience Cloud ID (ECID) for a user when using both AEP Edge extensions and Adobe Solutions extensions?
### A: Both identity extensions' ECID must be regenerated in sequence to avoid linking the old and new ECIDs in Adobe Experience Platform.

When using Real-time Customer Profile and Identity Service, the ECIDs from both identity extensions are linked together in the customer's Identity Graph. Care must be taken when regenerating new ECIDs such that the old and new ECIDs are not linked within the same Identity Graph.

Perform the following API calls to regenerate the ECIDs in sequence:
1. Set [privacy status](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr#set-and-get-privacy-status) to `optedOut` to clear the ECID from the AEP Identity direct service extension.
2. Call [resetIdentities](./edge-identity-api-reference#resetidentities) to regenerate a new ECID in the Identity for Edge Network extension.
3. Call [getExperienceCloudId](./edge-identity-api-reference#getexperiencecloudid) on the Identity for Edge Network extension. This ensures the new ECID is generated before continuing.
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


## Q: I would like to enable my XDM schema for Profile. Which identifier should be marked as primary?
### A: Only one identity in the IdentityMap may be marked primary.

{% hint style="info" %}
There can be only one primary identity per request event and the primary identity must be contained within the [IdentityMap](./edge-identity-api-reference#identitymap).
{% endhint %}

By default, the ECID from the Identity for Edge Network extension is the primary identifier for the Experience Event request. Once an Experience Event is received by the AEP Edge Network, if no identity is primary, it will mark the ECID as primary.

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

The [IdentityMap](./edge-identity-api-reference#identitymap) in the Identity for Edge Network extension is automatically included on each call to [Edge.sendEvent](../edge/edge-api-reference#sendevent). When using multiple Experience Data Model (XDM) schemas where each uses a different primary identifier, you will need to pass the primary identifier with each request, instead of marking a primary identifier in the Identity for Edge Network `IdentityMap`.

{% tabs %}
{% tab title="Android" %}
### Java

```java
// Sample example using Commerce schema
Map<String, Object> xdmData = new HashMap<String, Object>() {{
    put("identityMap", new HashMap<String, Object>() {{
        put("Email", new ArrayList<Object>() {{
            add(new HashMap<String, Object>() {{
                put("id", "user@example.com");
                put("authenticatedState", AuthenticatedState.AUTHENTICATED.getName());
                put("primary", true);
            }});
        }});
    }});
    put("commerce", new HashMap<String, Object>(){{
        put("productListViews", new HashMap<String, Object>() {{
            put("value", 1);
        }});
    }});
    put("productListItems", new ArrayList<Object>() {{
        add(new HashMap<String, Object>() {{
            put("SKU", "1002352692");
            put("product", "https://commerce.adobe.io/entities/product/product-203766910");
        }});
    }});
}};

// Create an Experience Event with the built schema and send it using the AEP Edge extension
ExperienceEvent event = new ExperienceEvent.Builder()
        .setXdmSchema(xdmData, "1234567890")
        .build();
Edge.sendEvent(event, null);
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

// Send event to the specified dataset
let experienceEvent = ExperienceEvent(xdm: xdmData, datasetIdentifier: "1234567890")
Edge.sendEvent(experienceEvent: experienceEvent)
```

### Objective-C

```objectivec
NSDictionary *commerce = @{@"productListViews": @{@"value": @1}};
NSArray *productListItems = @[@{
    @"SKU": @"1002352692",
    @"product": @"https://commerce.adobe.io/entities/product/product-203766910"
}];
NSDictionary *identityMap = @{@"Email": @[@{
    @"id":@"user@example.com",
    @"authenticatedState":@"authenticated",
    @"primary": @true
    
}]};

NSDictionary *xdmData = [[NSDictionary alloc] initWithObjectsAndKeys:identityMap,@"identityMap",commerce, @"commerce",productListItems,@"productListItems",nil];

AEPExperienceEvent *experienceEvent = [[AEPExperienceEvent alloc] initWithXdm:xdmData data:nil datasetIdentifier:@"1234567890"];
[AEPMobileEdge sendExperienceEvent:experienceEvent completion:nil];
```
{% endtab %}
{% endtabs %}
