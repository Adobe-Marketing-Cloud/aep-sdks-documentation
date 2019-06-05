# Identity API reference

## Sync identifiers

Updates the specified customer ID with the Adobe Experience Cloud ID service.

This API synchronizes the provided customer identifier type key and value with the [AuthenticationState](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#authenticationstate) to the Adobe Experience Cloud ID Service. If the specified customer ID type exists in the service, this ID type is updated with the new ID and authentication state. Otherwise, a new customer ID is added. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. If the current SDK privacy status is `optedout`, calling this method results in no operations being performed.

{% tabs %}
{% tab title="Android" %}
### syncIdentifier

#### **Syntax**

```text
public static void syncIdentifier(final String identifierType,
                                      final String identifier,
                                      final VisitorID.AuthenticationState authenticationState);
```

#### **Example**

```java
Identity.syncIdentifier("idType", "idValue", VisitorID.AuthenticationState.AUTHENTICATED);
```

### synchIdentifiers

**Tip**: The `identifiers` map contains IDs with the Identifier type as the key, and the string identifier as the value.

#### **Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers,
                                       final VisitorID.AuthenticationState authenticationState)
```

#### **Example**

```java
Map<String, String> identifiers = new HashMap<String, String>();
identifiers.put("idType", "idValue");
Identity.syncIdentifier(identifiers, VisitorID.AuthenticationState.AUTHENTICATED);
```

### synchIdentifiers \(overloaded\)

**Tip**: All given customer IDs are given the default authentication state of `UNKNOWN`.

These IDs are preserved between app upgrades, are saved and restored during the standard application backup process, and are removed at uninstall. If the current SDK privacy status is `optedout`, calling this method results in no operations being performed.

**Tip**: The `identifiers` dictionary contains IDs with the Identifier type as the key, and the string identifier as the value.

#### **Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers);
```

#### **Example**

```java
Map<String, String> identifiers = new HashMap<String, String>();
identifiers.put("idType", "idValue");
Identity.syncIdentifier(identifiers);
```
{% endtab %}

{% tab title="iOS" %}
### syncIdentifier

Updates the provided customer ID with the Adobe Experience Cloud ID Service.

This API synchronizes the provided customer identifier type key and value with the provided [authentication state](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#authenticationstate) to the Adobe Experience Cloud ID Service. If this customer ID type exists in the service, this type is updated with the new ID and authentication state. Otherwise a new customer ID is added. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. If the current SDK privacy status is `optedout`, calling this method results in no operations being performed.

#### **Syntax**

```objectivec
+ (void) syncIdentifier: (nonnull NSString*) identifierType             
             identifier: (nonnull NSString*) identifier
         authentication: (ADBMobileVisitorAuthenticationState) authenticationState;
```

#### **Examples**

**Objective-C**

```objectivec
[ACPIdentity syncIdentifier:@"idType" identifier:@"idValue" authentication:ACPMobileVisitorAuthenticationStateUnknown];
```

**Swift**

```swift
ACPIdentity.syncIdentifier("idType", identifier: "idValue", authentication: ACPMobileVisitorAuthenticationState.unknown)
```

## syncIdentifiers      <a id="syncidentifiers"></a>

Updates the provided customer IDs with the Adobe Experience Cloud ID Service.

This API synchronizes the provided customer identifiers to the Adobe Experience Cloud ID Service. If a customer ID type matches an existing ID type, it is updated with the new ID value and [authentication state](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#authenticationstate). New customer IDs are added. These IDs are preserved between app upgrades, are saved and restored during the standard application backup process, and are removed at uninstall. If the current SDK privacy status is `optedout`, calling this method results in no operations being performed.

**Tip**: The `identifiers` dictionary contains IDs with the Identifier type as the key, and the string identifier as the value.

#### **Syntax**

```objectivec
+ (void) syncIdentifiers: (nullable NSDictionary*) identifiers;
```

#### **Examples**

**Objective-C**

```objectivec
NSDictionary *ids = @{@"idType":@"idValue"};
[ACPIdentity syncIdentifiers:ids];
```

**Swift**

```swift
let identifiers : [String: String] = ["idType1":"idValue1", "idType2":"idValue2"];
ACPIdentity.syncIdentifiers(identifiers)
```

## syncIdentifiers \(overloaded\)      <a id="syncidentifiers-overloaded"></a>

Updates the provided customer IDs with the Adobe Experience Cloud ID Service.

This API synchronizes the provided customer identifiers to the Adobe Experience Cloud ID Service. If a customer ID type matches an existing ID type, the customer ID is updated with the new ID value and [authentication state](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#authenticationstate). New customer IDs are added. These IDs are preserved between app upgrades, are saved and restored during the standard application backup process, and are removed at uninstall. If the current SDK privacy status is `optedout`, calling this method results in no operations being performed.

**Tip**: The `identifiers` dictionary contains IDs with the Identifier type as the key, and the string identifier as the value.

### **Syntax**

```objectivec
+ (void) syncIdentifiers: (nullable NSDictionary*) identifiers          
         authentication: (ACPMobileVisitorAuthenticationState) authenticationState;
```

### **Examples**

**Objective-C**

```objectivec
NSDictionary *ids = @{@"idType":@"idValue"};
[ACPIdentity syncIdentifiers:ids authentication:ACPMobileVisitorAuthenticationStateAuthenticated];
```

**Swift**

```swift
let identifiers : [String: String] = ["idType1":"idValue1", "idType2":"idValue2"];ACPIdentity.syncIdentifiers(identifiers, authentication:
ACPMobileVisitorAuthenticationState.authenticated)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### syncIdentifier

Updates the provided customer ID with the Adobe Experience Cloud ID Service.

This API synchronizes the provided customer identifier type key and value with the provided [authentication state](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#authenticationstate) to the Adobe Experience Cloud ID Service. If this customer ID type exists in the service, this type is updated with the new ID and authentication state. Otherwise a new customer ID is added. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. If the current SDK privacy status is `optedout`, calling this method results in no operations being performed.

```jsx
ACPIdentity.syncIdentifier(identifierType, identifier, authenticationState);
```

### syncIdentifiers

```jsx
ACPIdentity.syncIdentifiers({"id1": "identifier1"});
```

### syncIdentifiersWithAuthState

```jsx
import {ACPMobileVisitorAuthenticationState} from '@adobe/react-native-acpcore';

ACPIdentity.syncIdentifiersWithAuthState({"id1": "identifier1"}, ACPMobileVisitorAuthenticationState.UNKNOWN);
```

Note: `ACPMobileVisitorAuthenticationState` contains the following getters:

```jsx
const AUTHENTICATED = "ACP_VISITOR_AUTH_STATE_AUTHENTICATED";
const LOGGED_OUT = "ACP_VISITOR_AUTH_STATE_LOGGED_OUT";
const UNKNOWN = "ACP_VISITOR_AUTH_STATE_UNKNOWN";
```
{% endtab %}
{% endtabs %}

## Append visitor data to a URL

{% tabs %}
{% tab title="Android" %}
### appendVisitorInfoForURL

Appends Adobe visitor data to a URL string. If the provided URL is null or empty, it is returned as is. Otherwise, the following information is added to the URL string that is returned in the [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback) instance:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](../../adobe-analytics/)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/174e9069bc1d3a521b59d52a066e9a7730f60ff5/using-mobile-extensions/adobe-analytics/analytics-api-reference/README.md#setidentifier).

#### **Syntax**

```java
public static void appendVisitorInfoForURL(final String baseURL, final AdobeCallback<String> callback);
```

#### **Example**

```java
Identity.appendVisitorInfoForURL("http://myurl.com", new AdobeCallback<String>() {    
    @Override    
    public void call(String urlWithAdobeVisitorInfo) {        
        //handle the new URL here        
        //For example, open the URL on the device browser        
        //        
        Intent i = new Intent(Intent.ACTION_VIEW);        
        i.setData(Uri.parse(urlWithAdobeVisitorInfo));        
        startActivity(i);    
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### appendToURL

Appends Adobe visitor data to a URL.

If the provided URL is nil or empty, it is returned as is. Otherwise, the following information is added to the url string that is returned via the callback:

* The adobe\_mc attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](../../adobe-analytics/)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/174e9069bc1d3a521b59d52a066e9a7730f60ff5/using-mobile-extensions/adobe-analytics/analytics-api-reference/README.md#setidentifier).

#### **Syntax**

```objectivec
+ (void) appendToUrl: (nullable NSURL*) baseUrl withCallback: (nullable void (^) (NSURL* __nullable urlWithVisitorData)) callback;
```

#### **Examples**

**Objective-C**

```objectivec
NSURL* url = [[NSURL alloc] initWithString:@"www.myUrl.com"];
[ACPIdentity appendToUrl:url withCallback:^(NSURL * _Nullable urlWithVisitorData) {    
// handle the appended url here}
}];
```

**Swift**

```swift
ACPIdentity.append(to:URL(string: "www.myUrl.com"), withCallback: {(appendedURL) in    
    // handle the appended url here

});
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### appendToURL

Appends Adobe visitor information to the given URL.

If the given url is nil or empty, it is returned as is. Otherwise, the following information is added to the query section of the given URL. The attribute `adobe_mc` is an URL encoded list containing the Experience Cloud ID, Experience Cloud Org ID, and a timestamp when this request was made. The attribute `adobe_aa_vid` is the URL encoded Visitor ID, however the attribute is only included if the Visitor ID was previously set.

```jsx
ACPIdentity.appendVisitorInfoForURL(baseURL);
```
{% endtab %}
{% endtabs %}

## Get visitor data as URL query parameter  <a id="getUrlVariablesTitle"></a>

{% tabs %}
{% tab title="Android" %}
### getUrlVariables

_added in Identity v1.1.0_

Retrieve Adobe visitor data as a URL query parameter string for consumption in hybrid mobile applications. There is no leading "?" or "&" punctuation, as the caller is responsible for placing the string in the correct location of their resulting URL. The following information is added to the string that is returned in the [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback) instance:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](../../adobe-analytics/)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/174e9069bc1d3a521b59d52a066e9a7730f60ff5/using-mobile-extensions/adobe-analytics/analytics-api-reference/README.md#setidentifier).

#### **Syntax**

```java
public static void getUrlVariables(final AdobeCallback<String> callback);
```

#### **Example**

```java
Identity.getUrlVariables(new AdobeCallback<String>() {    
    @Override    
    public void call(String stringWithAdobeVisitorInfo) {        
        //handle the URL query parameter string here 
        //For example, open the URL on the device browser        
        //        
        Intent i = new Intent(Intent.ACTION_VIEW);        
        i.setData(Uri.parse("http://myUrl.com?" + urlWithAdobeVisitorInfo));        
        startActivity(i);    
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### getUrlVariables

_added in ACPIdentity v2.1.0_

Retrieve Adobe visitor data as a URL query parameter string for consumption in hybrid mobile applications. There is no leading "?" or "&" punctuation, as the caller is responsible for placing the string in the correct location of their resulting URL. The following information is added to the string that is returned via the callback:

* The adobe\_mc attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](../../adobe-analytics/)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/174e9069bc1d3a521b59d52a066e9a7730f60ff5/using-mobile-extensions/adobe-analytics/analytics-api-reference/README.md#setidentifier).

#### **Syntax**

```objectivec
+ (void) getUrlVariables: (nonnull void (^) (NSString* __nullable urlVariables)) callback;
```

#### **Examples**

**Objective-C**

```objectivec
[ACPIdentity getUrlVariables:^(NSString * _Nullable urlVariables) {    
  // handle the URL query parameter string here
  NSString* urlString = @"http://myUrl.com";
  NSString* urlStringWithVisitorData = [NSString stringWithFormat:@"%@?%@", urlString, urlVariables];
  NSURL* urlWithVisitorData = [NSURL URLWithString:urlStringWithVisitorData];
  [[UIApplication sharedApplication] openURL:urlWithVisitorData options:@{} completionHandler:^(BOOL success) {
    // handle openURL success
  }];
}];
```

**Swift**

```swift
ACPIdentity.getUrlVariables {(urlVariables) in    
    // URL query parameter string
    let urlStringWithVisitorData : String = "http://myUrl.com?" + urlVariables!
    let urlWithVisitorData : NSURL = NSURL(string: urlStringWithVisitorData)!
    UIApplication.shared.open(urlWithVisitorData as URL, 
                              options: [:], 
                              completionHandler: {(complete) in 
                                 // handle open success
    })
}
```
{% endtab %}
{% endtabs %}

## Get identifiers

{% tabs %}
{% tab title="Android" %}
### getIdentifiers

Returns all customer identifiers that were previously synced with the Adobe Experience Cloud.

The values are returned through the [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback).

#### **Syntax**

```java
public static void getIdentifiers(final AdobeCallback<List<VisitorID>> callback);
```

#### **Example**

```java
Identity.getIdentifiers(new AdobeCallback<List<VisitorID>>() {    
    @Override    
    public void call(List<VisitorID> idList) {        
         //Process the IDs here    
    }

});
```
{% endtab %}

{% tab title="iOS" %}
### getIdentifiers

Returns all customer identifiers which were previously synced with the Adobe Experience Cloud.

#### **Syntax**

```objectivec
+ (void) getIdentifiers: (nonnull void (^) (NSArray<ADBMobileVisitorId*>* __nullable visitorIDs)) callback;
```

#### **Examples**

**Objective-C**

```objectivec
[ACPIdentity getIdentifiers:^(NSArray<ACPMobileVisitorId *> * _Nullable retrievedVisitorIds) {    
    // handle the retrieved Identifiers here     
    }];
```

**Swift**

```swift
ACPIdentity.getIdentifiers { (retrievedVisitorIds) in    
   // handle the retrieved Identifiers here        
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### getIdentifiers

Returns all customer identifiers which were previously synced with the Adobe Experience Cloud.

```jsx
ACPIdentity.getIdentifiers().then(identifiers => console.log("AdobeExperienceSDK: Identifiers = " + identifiers));
```
{% endtab %}
{% endtabs %}

## Get Experience Cloud IDs

{% tabs %}
{% tab title="Android" %}
### getExperienceCloudId

Retrieves the Experience Cloud ID from the Experience Cloud ID Service.

The Experience Cloud ID is generated at initial launch and is stored and used from that point forward. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. The values are returned via the [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback).

#### **Syntax**

```java
public static void getExperienceCloudId(final AdobeCallback<String> callback);
```

#### **Example**

```java
Identity.getExperienceCloudId(new AdobeCallback<String>() {    
    @Override    
    public void call(String id) {        
         //Handle the ID returned here    
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### getExperienceCloudId

Retrieves the Adobe Experience Cloud Visitor ID from the Adobe Experience Cloud ID Service.

The Experience Cloud ID is generated at initial launch and is stored and used from that point. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

#### **Syntax**

```objectivec
+ (void) getExperienceCloudId: (nonnull void (^) (NSString* __nullable experienceCloudId)) callback;
```

#### **Examples**

**Objective-C**

```objectivec
[ACPIdentity getExperienceCloudId:^(NSString * _Nullable retrievedCloudId) {    
// handle the retrieved Id here    
}];
```

**Swift**

```swift
ACPIdentity.getExperienceCloudId { (retrievedCloudId) in    
    // handle the retrieved Id here    
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### getExperienceCloudId

Retrieves the Adobe Experience Cloud Visitor ID from the Adobe Experience Cloud ID Service.

```jsx
ACPIdentity.getExperienceCloudId().then(cloudId => console.log("AdobeExperienceSDK: CloudID = " + cloudId));
```
{% endtab %}
{% endtabs %}

## Set an advertising identifier

The advertising ID is preserved between app upgrades, is saved and restored during the standard application backup process, available via [Signals](../signals/), and is removed at uninstall.

{% hint style="info" %}
If the current SDK privacy status is `optedout`, the advertising identifier is not set or stored.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

### setAdvertisingIdentifier

#### **Syntax**

```java
public static void setAdvertisingIdentifier(final String advertisingIdentifier);
```

#### **Example**

```java
MobileCore.setAdvertisingIdentifier("advertising_identifier");
```
{% endtab %}

{% tab title="iOS" %}
### setAdvertisingIdentifier

#### **Objective C**

#### **Syntax**

```objectivec
+ (void) setAdvertisingIdentifier: (nullable NSString*) adId;
```

Examples

```objectivec
[ACPCore setAdvertisingIdentifier:@"AdvertisingId"];
```

**Swift**

```swift
ACPCore.setAdvertisingIdentifier("AdvertisingId")
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### setAdvertisingIdentifier

```jsx
ACPCore.setAdvertisingIdentifier("adID");
```
{% endtab %}
{% endtabs %}

## Set the push identifier

This API sets the device token for push notifications in the SDK. If the current SDK privacy status is `optedout`, the push identifier is not set.

{% tabs %}
{% tab title="Android" %}
### setPushIdentifier

#### **Syntax**

```java
public static void setPushIdentifier(final String pushIdentifier);
```

#### **Example**

```java
//Retrieve the token from either GCM or FCM, and pass it to the SDK
MobileCore.setPushIdentifier(token);
```
{% endtab %}

{% tab title="iOS" %}
### setPushIdentifier

#### **Objective-C**

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

Example

```objectivec
// Set the deviceToken that the APNS has assigned to the device
[ACPCore setPushIdentifier:deviceToken];
```

#### **Swift**

```swift
// Set the deviceToken that the APNs has assigned to the device
ACPCore.setPushIdentifier(deviceToken)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### setPushIdentifier

```jsx
ACPCore.setPushIdentifier("pushIdentifier");
```
{% endtab %}
{% endtabs %}

## Identity service classes

{% tabs %}
{% tab title="Android" %}
### AdobeCallback      <a id="adobecallback"></a>

This class provides the interface to receive results when the async APIs perform the requested action.

```java
public interface AdobeCallback<T> {    
    void call(final T value);
}
```

### VisitorID      <a id="visitorid"></a>

An identifier to be used with the Experience Cloud Visitor ID Service.

```java
public class VisitorID {    
     //Constructor    
     public VisitorID(String idOrigin, String idType, String id, VisitorID.AuthenticationState authenticationState);​    

     public VisitorID.AuthenticationState getAuthenticationState();​    

     public final String getId();​    

     public final String getIdOrigin();​    

     public final String getIdType();​​

}
```

### AuthenticationState      <a id="authenticationstate"></a>

Used to indicate the authentication state for the current `VisitorID`.

```java
public enum AuthenticationState {        
       UNKNOWN,        
       AUTHENTICATED,        
       LOGGED_OUT;
}
```
{% endtab %}

{% tab title="iOS" %}
### ACPMobileVisitorId

An identifier to be used with the Experience Cloud Visitor ID Service.

Contains the origin, the type, a value, and the authentication state of the visitor ID.

```objectivec
@interface ACPMobileVisitorId : NSObject​

@property(nonatomic, strong, nullable) NSString* idOrigin;
@property(nonatomic, strong, nullable) NSString* idType;
@property(nonatomic, strong, nullable) NSString* identifier;
@property(nonatomic, readwrite) ACPMobileVisitorAuthenticationState authenticationState;​

@end
```

### ACPMobileVisitorAuthenticationState      <a id="acpmobilevisitorauthenticationstate"></a>

Used to indicate the authentication state for the current `VisitorID`.

```objectivec
typedef NS_ENUM(NSUInteger,
    ADBMobileVisitorAuthenticationState) {    
    ACPMobileVisitorAuthenticationStateUnknown          = 0,    
    ACPMobileVisitorAuthenticationStateAuthenticated    = 1,    
    ACPMobileVisitorAuthenticationStateLoggedOut        = 2  };
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### ACPVisitorID

```jsx
import {ACPVisitorID} from '@adobe/react-native-acpcore';

var visitorId = new ACPVisitorID(idOrigin?: string, idType: string, id?: string, authenticationState?: ACPMobileVisitorAuthenticationState)
```
{% endtab %}
{% endtabs %}

