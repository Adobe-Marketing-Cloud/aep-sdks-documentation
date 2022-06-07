# API Reference

## extensionVersion

The extensionVersion() API returns the version of the Identity for Edge Network extension.

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
public static String extensionVersion()
```
**Example**

```java
String extensionVersion = Identity.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static var extensionVersion: String
```
**Examples**

```swift
let extensionVersion = EdgeIdentity.extensionVersion
```

### Objective-C

**Syntax**

```objectivec
+ (nonnull NSString*) extensionVersion;
```

**Examples**

```objectivec
NSString *extensionVersion = [AEPMobileEdgeIdentity extensionVersion];
```
{% endtab %}
{% endtabs %}

## getExperienceCloudId

This API retrieves the Experience Cloud ID (ECID) that was generated when the app was initially launched. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

{% tabs %}
{% tab title="Android" %}

The ECID value is returned via the [AdobeCallback](../mobile-core/mobile-core-api-reference.md#public-classes). When [AdobeCallbackWithError](../mobile-core/mobile-core-api-reference.md#public-classes) is provided to this API, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core/mobile-core-api-reference.md#public-classes).

### Java

**Syntax**

```java
public static void getExperienceCloudId(final AdobeCallback<String> callback);
```

* _callback_ is invoked after the ECID is available. The callback may be invoked on a different thread.

**Example**

```java
Identity.getExperienceCloudId(new AdobeCallback<String>() {    
    @Override    
    public void call(String id) {        
         //Handle the ID returned here    
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static func getExperienceCloudId(completion: @escaping (String?, Error?) -> Void)
```

* _completion_ is invoked after the ECID is available.  The default timeout is 1000ms.

**Examples**

```swift
Identity.getExperienceCloudId { (ecid, error) in
  if let error = error {
    // handle error here
  } else {
    // handle the retrieved ID here
  }
}
```
### Objective-C

**Syntax**

```objectivec
+ (void) getExperienceCloudId:^(NSString * _Nullable ecid, NSError * _Nullable error)completion
```
**Examples**

```objectivec
[AEPMobileEdgeIdentity getExperienceCloudId:^(NSString *ecid, NSError *error) {   
    // handle the error and the retrieved ID here    
}];
```

{% endtab %}
{% endtabs %}

## getIdentities

Get all identities in the Identity for Edge Network extension, including customer identifiers which were previously added.

{% tabs %}
{% tab title="Android" %}

When [AdobeCallbackWithError](../mobile-core/mobile-core-api-reference.md#public-classes) is provided, and you are fetching the identities from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core/mobile-core-api-reference.md#public-classes).

### Java

**Syntax**

```java
public static void getIdentities(final AdobeCallback<IdentityMap> callback);
```

* _callback_ is invoked after the identities are available. The return format is an instance of [IdentityMap](api-reference.md#identitymap). The callback may be invoked on a different thread.

**Example**

```java
Identity.getIdentities(new AdobeCallback<IdentityMap>() {    
    @Override    
    public void call(IdentityMap identityMap) {        
         //Handle the IdentityMap returned here    
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static func getIdentities(completion: @escaping (IdentityMap?, Error?) -> Void)
```

* _completion_ is invoked after the identities are available.  The default timeout is 1000ms. The return format is an instance of [IdentityMap](api-reference.md#identitymap).

**Examples**

```swift
Identity.getIdentities { (identityMap, error) in
  if let error = error {
    // handle error here
  } else {
    // handle the retrieved identitites here
  }
}
```

### Objective-C

**Syntax**

```objectivec
+ (void) getIdentities:^(AEPIdentityMap * _Nullable map, NSError * _Nullable error)completion
```

**Examples**

```objectivec
[AEPMobileEdgeIdentity getIdentities:^(AEPIdentityMap *map, NSError *error) {   
    // handle the error and the retrieved ID here
}];
```

{% endtab %}
{% endtabs %}


## registerExtension

Registers the Identity for Edge Network extension with the Mobile Core extension.

{% hint style="info" %}
If your use-case covers both Edge Network and Adobe Experience Cloud Solutions extensions, you need to register Identity for Edge Network and Identity for Experience Cloud Identity Service from Mobile Core extensions. For more details, see the [frequently asked questions](identity-faq.md#q-i-am-using-aep-edge-and-adobe-solutions-extensions-which-identity-extension-should-i-install-and-register).

{% endhint %}

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
public static void registerExtension()
```

**Example**
```java
import com.adobe.marketing.mobile.edge.identity.Identity

...
Identity.registerExtension();
```

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

In iOS, the registration occurs by passing Identity for Edge Network extension to the [MobileCore.registerExtensions API](../mobile-core/mobile-core-api-reference.md#registerextension-s).

### Swift

**Syntax**

```swift
static func registerExtensions(_ extensions: [NSObject.Type], 
                               _ completion: (() -> Void)? = nil)
```

**Examples**

```swift
import AEPEdgeIdentity

...
MobileCore.registerExtensions([Identity.self])
```

### Objective-C

**Syntax**

```objectivec
+ (void) registerExtensions: (NSArray<Class*>* _Nonnull) extensions 
                 completion: (void (^ _Nullable)(void)) completion;
```
**Examples**

```objectivec
@import AEPEdgeIdentity;

...
[AEPMobileCore registerExtensions:@[AEPMobileEdgeIdentity.class] completion:nil];
```

{% endtab %}
{% endtabs %}

## removeIdentity

Remove the identity from the stored client-side [IdentityMap](api-reference.md#identitymap). The Identity extension will stop sending the identifier to the Edge Network. Using this API does not remove the identifier from the server-side User Profile Graph or Identity Graph.

Identities with an empty _id_ or _namespace_ are not allowed and are ignored.

Removing identities using a reserved namespace is not allowed using this API. The reserved namespaces are:

* ECID
* IDFA
* GAID

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
public static void removeIdentity(final IdentityItem item, final String namespace);
```

**Example**

```java
IdentityItem item = new IdentityItem("user@example.com");
Identity.removeIdentity(item, "Email");
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static func removeIdentity(item: IdentityItem, withNamespace: String)
```

**Examples**

```swift
Identity.removeIdentity(item: IdentityItem(id: "user@example.com"), withNamespace: "Email")
```

### Objective-C

**Syntax**

```objectivec
+ (void) removeIdentityItem:(AEPIdentityItem * _Nonnull) item 
                             withNamespace: (NSString * _Nonnull) namespace
```

**Examples**

```objectivec
AEPIdentityItem *item = [[AEPIdentityItem alloc] initWithId:@"user@example.com" authenticatedState:AEPAuthenticatedStateAuthenticated primary:false];
[AEPMobileEdgeIdentity removeIdentityItem:item withNamespace:@"Email"];
```

{% endtab %}
{% endtabs %}

## resetIdentities

Clears all identities stored in the Identity extension and generates a new Experience Cloud ID (ECID). Using this API does not remove the identifiers from the server-side User Profile Graph or Identity Graph.

This is a destructive action, since once an ECID is removed it cannot be reused. The new ECID generated by this API can increase metrics like unique visitors when a new user profile is created.

Some example use cases for this API are: 
* During debugging, to see how new ECIDs (and other identifiers paired with it) behave with existing rules and metrics.
* A last-resort reset for when an ECID should no longer be used.

This API is not recommended for:
* Resetting a user's consent and privacy settings; see [Privacy and GDPR](../../resources/privacy-and-gdpr.md).
* Removing existing custom identifiers; use the [`removeIdentity`](#removeidentity) API instead.
* Removing a previously synced advertising identifier after the advertising tracking settings were changed by the user; use the [`setAdvertisingIdentifier`](../mobile-core/identity/identity-api-reference.md#setadvertisingidentifier) API instead.


{% hint style="warning" %}
The Identity for Edge Network extension does not read the Mobile SDK's privacy status, and therefore setting the SDK's privacy status to opt-out will not automatically clear the identities from the Identity for Edge Network extension.
{% endhint %}

See [`MobileCore.resetIdentities`](../mobile-core/mobile-core-api-reference.md#resetidentities) for more details.

## setAdvertisingIdentifier
When this API is called with a valid advertising identifier, the Identity for Edge Network extension includes the advertising identifier in the XDM Identity Map using the namespace `GAID` (Google Advertising ID) in Android and `IDFA` (Identifier for Advertisers) in iOS. If the API is called with the empty string (`""`), `null`/`nil`, or the all-zeros UUID string values, the advertising identifier is removed from the XDM Identity Map (if previously set).

The advertising identifier is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

{% tabs %}
{% tab title="Android" %}

{% hint style="warning" %}
In order to enable collection of the user's current advertising tracking authorization selection for the provided advertising identifier, you need to install and register the [AEPEdgeConsent](../consent-for-edge-network/README.md) extension and update the [AEPEdge](../experience-platform-extension/README.md) dependency to minimum 1.3.2.
{% endhint %}

{% hint style="info" %}
These examples require Google Play Services to be configured in your mobile application and use the Google Mobile Ads Lite SDK. For instructions on how to import the SDK and configure your `ApplicationManifest.xml` file see [Google Mobile Ads Lite SDK setup](https://developers.google.com/admob/android/lite-sdk).
{% endhint %}

{% hint style="info" %}
These are just implementation examples. For more information about advertising identifiers and how to handle them correctly in your mobile application see [Google Play Services documentation about AdvertisingIdClient](https://developers.google.com/android/reference/com/google/android/gms/ads/identifier/AdvertisingIdClient).
{% endhint %}

### Java

**Syntax**

```java
public static void setAdvertisingIdentifier(final String advertisingIdentifier);
```
- _advertisingIdentifier_ is an ID string that provides developers with a simple, standard system to continue to track ads throughout their apps.

**Example**

```java
...
@Override
public void onResume() {
    super.onResume();
    ...
    new Thread(new Runnable() {
        @Override
        public void run() {
            String advertisingIdentifier = null;

            try {
                AdvertisingIdClient.Info adInfo = AdvertisingIdClient.getAdvertisingIdInfo(getApplicationContext());
                if (adInfo != null) {
                    if (!adInfo.isLimitAdTrackingEnabled()) {
                        advertisingIdentifier = adInfo.getId();
                    } else {
                        MobileCore.log(LoggingMode.DEBUG, "ExampleActivity", "Limit Ad Tracking is enabled by the user, cannot process the advertising identifier");
                    }
                }

            } catch (IOException e) {
                // Unrecoverable error connecting to Google Play services (e.g.,
                // the old version of the service doesn't support getting AdvertisingId).
                MobileCore.log(LoggingMode.DEBUG, "ExampleActivity", "IOException while retrieving the advertising identifier " + e.getLocalizedMessage());
            } catch (GooglePlayServicesNotAvailableException e) {
                // Google Play services is not available entirely.
                MobileCore.log(LoggingMode.DEBUG, "ExampleActivity", "GooglePlayServicesNotAvailableException while retrieving the advertising identifier " + e.getLocalizedMessage());
            } catch (GooglePlayServicesRepairableException e) {
                // Google Play services is not installed, up-to-date, or enabled.
                MobileCore.log(LoggingMode.DEBUG, "ExampleActivity", "GooglePlayServicesRepairableException while retrieving the advertising identifier " + e.getLocalizedMessage());
            }

            MobileCore.setAdvertisingIdentifier(advertisingIdentifier);
        }
    }).start();
}
```

### Kotlin

**Syntax**

```kotlin
public fun setAdvertisingIdentifier(advertisingIdentifier: String)
```
- _advertisingIdentifier_ is an ID string that provides developers with a simple, standard system to continue to track ads throughout their apps.

**Example**
  
```kotlin
import android.content.Context
import android.util.Log
import com.google.android.gms.ads.identifier.AdvertisingIdClient
import com.google.android.gms.common.GooglePlayServicesNotAvailableException
import com.google.android.gms.common.GooglePlayServicesRepairableException
import java.io.IOException
...

suspend fun getGAID(applicationContext: Context): String {
    var adID = ""
    try {
        val idInfo = AdvertisingIdClient.getAdvertisingIdInfo(applicationContext)
        if (idInfo.isLimitAdTrackingEnabled) {
            Log.d("ExampleActivity", "Limit Ad Tracking is enabled by the user, setting ad ID to \"\"")
            return adID
        }
        Log.d("ExampleActivity", "Limit Ad Tracking disabled; ad ID value: ${idInfo.id}")
        adID = idInfo.id
    } catch (e: GooglePlayServicesNotAvailableException) {
        Log.d("ExampleActivity", "GooglePlayServicesNotAvailableException while retrieving the advertising identifier ${e.localizedMessage}")
    } catch (e: GooglePlayServicesRepairableException) {
        Log.d("ExampleActivity", "GooglePlayServicesRepairableException while retrieving the advertising identifier ${e.localizedMessage}")
    } catch (e: IOException) {
        Log.d("ExampleActivity", "IOException while retrieving the advertising identifier ${e.localizedMessage}")
    }
    Log.d("ExampleActivity", "Returning ad ID value: $adID")
    return adID
}
```

Call site:

```kotlin
import kotlinx.coroutines.CoroutineScope
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.launch
...

 // Create background coroutine scope to fetch ad ID value
val scope = CoroutineScope(Dispatchers.IO).launch {
    val adID = sharedViewModel.getGAID(context.applicationContext)
    Log.d("ExampleActivity", "Sending ad ID value: $adID to MobileCore.setAdvertisingIdentifier")
    MobileCore.setAdvertisingIdentifier(adID)
}
```

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

{% hint style="warning" %}
In order to enable the collection of current advertising tracking user's selection based on the provided advertising identifier, you need to install and register the [AEPEdgeConsent](../consent-for-edge-network/README.md) extension and update the [AEPEdge](../experience-platform-extension/README.md) dependency to minimum 1.4.1. 
{% endhint %}

{% hint style="warning" %}
Starting iOS 14+, applications must use the [App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency) framework to request user authorization before using the Identifier for Advertising (IDFA). To access IDFA and handle it correctly in your mobile application, see the [Apple developer documentation about IDFA](https://developer.apple.com/documentation/adsupport/asidentifiermanager). 
{% endhint %}

### Swift

**Syntax**

```swift
@objc(setAdvertisingIdentifier:)
public static func setAdvertisingIdentifier(_ identifier: String?)
```
- _identifier_ is an ID string that provides developers with a simple, standard system to continue to track ads throughout their apps.

**Example**

```swift
import AdSupport
import AppTrackingTransparency
...

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    ...
    if #available(iOS 14, *) {
       setAdvertisingIdentifierUsingTrackingManager()
    } else {
       // Fallback on earlier versions
       setAdvertisingIdentifierUsingIdentifierManager()
    }

}

func setAdvertisingIdentifierUsingIdentifierManager() {
    var idfa:String = "";
        if (ASIdentifierManager.shared().isAdvertisingTrackingEnabled) {
            idfa = ASIdentifierManager.shared().advertisingIdentifier.uuidString;
        } else {
            Log.debug(label: "AppDelegateExample",
                      "Advertising Tracking is disabled by the user, cannot process the advertising identifier.");
        }
        MobileCore.setAdvertisingIdentifier(idfa);
}

@available(iOS 14, *)
func setAdvertisingIdentifierUsingTrackingManager() {
    ATTrackingManager.requestTrackingAuthorization { (status) in
        var idfa: String = "";

        switch (status) {
        case .authorized:
            idfa = ASIdentifierManager.shared().advertisingIdentifier.uuidString
        case .denied:
            Log.debug(label: "AppDelegateExample",
                      "Advertising Tracking is denied by the user, cannot process the advertising identifier.")
        case .notDetermined:
            Log.debug(label: "AppDelegateExample",
                      "Advertising Tracking is not determined, cannot process the advertising identifier.")
        case .restricted:
            Log.debug(label: "AppDelegateExample",
                      "Advertising Tracking is restricted by the user, cannot process the advertising identifier.")
        }

        MobileCore.setAdvertisingIdentifier(idfa)
    }
}
```

### Objective-C

**Syntax**

```objectivec
+ (void) setAdvertisingIdentifier: (NSString * _Nullable identifier);
```

- _identifier_ is an ID string that provides developers with a simple, standard system to continue to track ads throughout their apps.

**Example**

```objectivec
#import <AdSupport/ASIdentifierManager.h>
#import <AppTrackingTransparency/ATTrackingManager.h>
...

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
-   ...
-   
    if (@available(iOS 14, *)) {
        [self setAdvertisingIdentifierUsingTrackingManager];
    } else {
        // fallback to earlier versions
        [self setAdvertisingIdentifierUsingIdentifierManager];
    }

}

- (void) setAdvertisingIdentifierUsingIdentifierManager {
    // setup the advertising identifier
    NSString *idfa = nil;
    if ([[ASIdentifierManager sharedManager] isAdvertisingTrackingEnabled]) {
        idfa = [[[ASIdentifierManager sharedManager] advertisingIdentifier] UUIDString];
    } else {
        [AEPLog debugWithLabel:@"AppDelegateExample"
                       message:@"Advertising Tracking is disabled by the user, cannot process the advertising identifier"];
    }
    [AEPMobileCore setAdvertisingIdentifier:idfa];

}

- (void) setAdvertisingIdentifierUsingTrackingManager API_AVAILABLE(ios(14)) {
    [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:
    ^(ATTrackingManagerAuthorizationStatus status){
        NSString *idfa = nil;
        switch(status) {
            case ATTrackingManagerAuthorizationStatusAuthorized:
                idfa = [[[ASIdentifierManager sharedManager] advertisingIdentifier] UUIDString];
                break;
            case ATTrackingManagerAuthorizationStatusDenied:
                [AEPLog debugWithLabel:@"AppDelegateExample"
                               message:@"Advertising Tracking is denied by the user, cannot process the advertising identifier"];
                break;
            case ATTrackingManagerAuthorizationStatusNotDetermined:
                [AEPLog debugWithLabel:@"AppDelegateExample"
                               message:@"Advertising Tracking is not determined, cannot process the advertising identifier"];
                break;
            case ATTrackingManagerAuthorizationStatusRestricted:
                [AEPLog debugWithLabel:@"AppDelegateExample"
                               message:@"Advertising Tracking is restricted by the user, cannot process the advertising identifier"];
                break;
        }

        [AEPMobileCore setAdvertisingIdentifier:idfa];
    }];
}
```

{% endtab %}
{% endtabs %}

## updateIdentities

Update the currently known identities within the SDK. The Identity extension will merge the received identifiers with the previously saved ones in an additive manner; no identities are removed by this API.

Identities with an empty _id_ or _namespace_ are not allowed and are ignored.

Updating identities using a reserved namespace is not allowed using this API. The reserved namespaces are:

* ECID
* IDFA
* GAID

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
public static void updateIdentities(final IdentityMap identityMap);
```

**Example**

```java
IdentityItem item = new IdentityItem("user@example.com");
IdentityMap identityMap = new IdentityMap();
identityMap.addItem(item, "Email")
Identity.updateIdentities(identityMap);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static func updateIdentities(with map: IdentityMap)
```

**Examples**

```swift
let identityMap = IdentityMap()
map.addItem(item: IdentityItem(id: "user@example.com"), withNamespace: "Email")
Identity.updateIdentities(with: identityMap)
```

### Objective-C

**Syntax**

```objectivec
+ (void) updateIdentities:(AEPIdentityMap * _Nonnull)map
```

**Examples**

```objectivec
AEPIdentityItem *item = [[AEPIdentityItem alloc] initWithId:@"user@example.com" authenticatedState:AEPAuthenticatedStateAuthenticated primary:false];
AEPIdentityMap *map = [[AEPIdentityMap alloc] init];
[map addItem:item withNamespace:@"Email"];
[AEPMobileEdgeIdentity updateIdentities:map];
```

{% endtab %}
{% endtabs %}

## Public Classes

### IdentityMap

Defines a map containing a set of end user identities, keyed on either namespace integration code or the namespace ID of the identity. The values of the map are an array, meaning that more than one identity of each namespace may be carried.

The format of the IdentityMap class is defined by the [XDM Identity Map Schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/shared/identitymap.schema.md).

For more information, please read an overview of the [AEP Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html).

```text
"identityMap" : {
    "Email" : [
      {
        "id" : "user@example.com",
        "authenticatedState" : "authenticated",
        "primary" : false
      }
    ],
    "Phone" : [
      {
        "id" : "1234567890",
        "authenticatedState" : "ambiguous",
        "primary" : false
      },
      {
        "id" : "5557891234",
        "authenticatedState" : "ambiguous",
        "primary" : false
      }
    ],
    "ECID" : [
      {
        "id" : "44809014977647551167356491107014304096",
        "authenticatedState" : "ambiguous",
        "primary" : true
      }
    ]
  }
```

{% tabs %}

{% tab title="Android" %}

### Java

**Example**

```java
// Construct
IdentityMap identityMap = new IdentityMap();

// Add an item
IdentityItem item = new IdentityItem("user@example.com");
identityMap.addItem(item, "Email");

// Remove an item
IdentityItem item = new IdentityItem("user@example.com");
identityMap.removeItem(item, "Email");

// Get a list of items for a given namespace
List<IdentityItem> items = identityMap.getIdentityItemsForNamespace("Email");

// Get a list of all namespaces used in current IdentityMap
List<String> namespaces = identityMap.getNamespaces();

// Check if IdentityMap has no identities
boolean hasNotIdentities = identityMap.isEmpty();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Example**

```swift
// Initialize
let identityMap: IdentityMap = IdentityMap()

// Add an item
identityMap.add(item: IdentityItem(id: "user@example.com"), withNamespace: "Email")

// Remove an item
identityMap.remove(item: IdentityItem(id: "user@example.com", withNamespace: "Email"))

// Get a list of items for a given namespace
let items: [IdentityItem] = identityMap.getItems(withNamespace: "Email")

// Get a list of all namespaces used in current IdentityMap
let namespaces: [String] = identityMap.namespaces

// Check if IdentityMap has no identities
let hasNoIdentities: Bool = identityMap.isEmpty
```
### Objective-C

**Example**

```objectivec
// Initialize
AEPIdentityMap* identityMap = [[AEPIdentityMap alloc] init];

// Add an item
AEPIdentityItem* item = [[AEPIdentityItem alloc] initWithId:@"user@example.com" authenticatedState:AEPAuthenticatedStateAuthenticated primary:false];
[identityMap addItem:item withNamespace:@"Email"];

// Remove an item
AEPIdentityItem* item = [[AEPIdentityItem alloc] initWithId:@"user@example.com" authenticatedState:AEPAuthenticatedStateAuthenticated primary:false];
[identityMap removeItem:item withNamespace:@"Email"];

// Get a list of items for a given namespace
NSArray<AEPIdentityItem*>* items = [identityMap getItemsWithNamespace:@"Email"];

// Get a list of all namespaces used in current IdentityMap
NSArray<NSString*>* namespaces = identityMap.namespaces;

// Check if IdentityMap has no identities
bool hasNoIdentities = identityMap.isEmpty;
```

{% endtab %}
{% endtabs %}

### IdentityItem

Defines an identity to be included in an [IdentityMap](api-reference.md#identitymap).

The format of the IdentityItem class is defined by the [XDM Identity Item Schema](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/identityitem.schema.md).

{% tabs %}
{% tab title="Android" %}

### Java

**Example**

```java
// Construct
IdentityItem item = new IdentityItem("identifier");

IdentityItem item = new IdentityItem("identifier", AuthenticatedState.AUTHENTICATED, false);


// Getters
String id = item.getId();

AuthenticatedState state = item.getAuthenticatedState();

boolean primary = item.isPrimary();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Example**

```swift
// Initialize
let item = IdentityItem(id: "identifier")

let item = IdentityItem(id: "identifier", authenticatedState: .authenticated, primary: false)

// Getters
let id: String = item.id

let state: AuthenticatedState = item.authenticatedState

let primary: Bool = item.primary
```
### Objective-C

**Example**

```objectivec
// Initialize
AEPIdentityItem* item = [[AEPIdentityItem alloc] initWithId:@"identity" authenticatedState:AEPAuthenticatedStateAuthenticated primary:false];

// Getters
NSString* id = primaryEmail.id;

long state = primaryEmail.authenticatedState;

bool primary = primaryEmail.primary;
```

{% endtab %}
{% endtabs %}

### AuthenticatedState

Defines the state an [Identity Item](api-reference.md#identityitem) is authenticated for.

The possible authenticated states are:

* Ambiguous - the state is ambiguous or not defined
* Authenticated - the user is identified by a login or similar action
* LoggedOut - the user was identified by a login action at a previous time, but is not logged in now

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public enum AuthenticatedState {
    AMBIGUOUS("ambiguous"),
    AUTHENTICATED("authenticated"),
    LOGGED_OUT("loggedOut");
}
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
**Syntax**

```swift
@objc(AEPAuthenticatedState)
public enum AuthenticatedState: Int, RawRepresentable, Codable {
    case ambiguous = 0
    case authenticated = 1
    case loggedOut = 2
}
```
{% endtab %}
{% endtabs %}