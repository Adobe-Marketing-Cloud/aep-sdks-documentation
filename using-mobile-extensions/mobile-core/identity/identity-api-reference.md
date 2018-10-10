# Identity API Reference

## Synch Identifiers

Updates the specified customer ID with the Adobe Experience Cloud ID service.

This API synchronizes the provided customer identifier type key and value with the given [authentication state](https://docs.adobelaunch.com/extension-reference/mobile/identity/identity-methods-in-android#authenticationstate) to the Adobe Experience Cloud ID Service. If the specified customer ID type exists in the service, this ID type is updated with the new ID and authentication state. Otherwise, a new customer ID is added. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. If the current SDK privacy status is `optedout`, calling this method results in no operations being performed.

{% tabs %}
{% tab title="Android" %}
### syncidentifier

**Syntax**

```text
public static void syncIdentifier(final String identifierType,
                                      final String identifier,
                                      final VisitorID.AuthenticationState authenticationState);

```

**Example**

```java
Identity.syncIdentifier("idType", "idValue", VisitorID.AuthenticationState.AUTHENTICATED);
```

### synchidentifiers

**Tip**: The `identifiers` map contains IDs with the Identifier type as the key, and the string identifier as the value.

**Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers,
                                       final VisitorID.AuthenticationState authenticationState)
```

**Example**

```java
Map<String, String> identifiers = new HashMap<String, String>();
identifiers.put("idType", "idValue");
Identity.syncIdentifier(identifiers, VisitorID.AuthenticationState.AUTHENTICATED);
```

### synchidentifiers \(overloaded\)

**Tip**: All given customer IDs are given the default authentication state of `UNKNOWN`.

These IDs are preserved between app upgrades, are saved and restored during the standard application backup process, and are removed at uninstall. If the current SDK privacy status is `optedout`, calling this method results in no operations being performed.

**Tip**: The `identifiers` dictionary contains IDs with the Identifier type as the key, and the string identifier as the value.

**Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers);
```

**Example**

```java
Map<String, String> identifiers = new HashMap<String, String>();
identifiers.put("idType", "idValue");
Identity.syncIdentifier(identifiers);
```
{% endtab %}

{% tab title="iOS" %}
### synchidentifier
{% endtab %}
{% endtabs %}

## Append Visitor Data to a URL

{% tabs %}
{% tab title="Android" %}
### appendVisitorInfoForURL

Appends Adobe visitor data to a URL string. If the provided URL is null or empty, it is returned as is. Otherwise, the following information is added to the url string that is returned in the [AdobeCallback](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/identity/identity-methods-in-android#adobecallback) instance:

* The `adobe_mc` attribute is an URL encoded list containing:
  * Experience Cloud ID \(ECID\)
  * Experience Cloud Org ID
  * A timestamp taken when this request was made
* The optional adobe\_aa\_vid attribute is the URL encoded Analytics Custom Visitor ID, if available

### **Syntax** {#syntax-3}

```java
public static void appendVisitorInfoForURL(final String baseURL, final AdobeCallback<String> callback);
```

### **Example** {#example-3}

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

* The adobe\_mc attribute is an URL encoded list containing:
  * Experience Cloud ID \(ECID\)
  * Experience Cloud Org ID
  * A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID, if available.

### **Syntax** {#syntax-3}

```objectivec
+ (void) appendToUrl: (nullable NSURL*) baseUrl withCallback: (nullable void (^) (NSURL* __nullable urlWithVisitorData)) callback;
```

### **Examples** {#examples-3}

#### Objective-C {#objective-c-3}

```objectivec
NSURL* url = [[NSURL alloc] initWithString:@"www.myUrl.com"];
[ACPIdentity appendToUrl:url withCallback:^(NSURL * _Nullable urlWithVisitorData) {    
// handle the appended url here}
];
```

#### Swift {#swift-3}

```swift
ACPIdentity.append(to:URL(string: "www.myUrl.com"), withCallback: {(appendedURL) in    
    // handle the appended url here

});
```
{% endtab %}
{% endtabs %}

## Get Identifiers

{% tabs %}
{% tab title="Android" %}
### getIdentifiers

Returns all customer identifiers which were previously synced with the Adobe Experience Cloud.

The values are returned through the [AdobeCallback](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/identity/identity-methods-in-android#adobecallback).

### **Syntax** {#syntax-4}

```java
public static void getIdentifiers(final AdobeCallback<List<VisitorID>> callback);
```

### **Example** {#example-4}

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

### **Syntax** {#syntax-4}

```objectivec
+ (void) getIdentifiers: (nonnull void (^) (NSArray<ADBMobileVisitorId*>* __nullable visitorIDs)) callback;
```

### **Examples** {#examples-4}

#### Objective-C {#objective-c-4}

```objectivec
[ACPIdentity getIdentifiers:^(NSArray<ACPMobileVisitorId *> * _Nullable retrievedVisitorIds) {    
    // handle the retrieved Identifiers here     
    }];
```

#### Swift {#swift-4}

```swift
ACPIdentity.getIdentifiers { (retrievedVisitorIds) in    
   // handle the retrieved Identifiers here        
}
```
{% endtab %}
{% endtabs %}

## Get Experience Cloud IDs

{% tabs %}
{% tab title="Android" %}
### getExperienceCloudId

Retrieves the Experience Cloud ID from the Experience Cloud ID Service.

The Experience Cloud ID is generated at initial launch and is stored and used from that point forward. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. The values are returned via the [AdobeCallback](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/identity/identity-methods-in-android#adobecallback).

### **Syntax** {#syntax-5}

```java
public static void getExperienceCloudId(final AdobeCallback<String> callback);
```

### **Example** {#example-5}

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

### **Syntax** {#syntax-5}

```objectivec
+ (void) getExperienceCloudId: (nonnull void (^) (NSString* __nullable experienceCloudId)) callback;
```

### **Examples** {#examples-5}

#### Objective-C {#objective-c-5}

```objectivec
[ACPIdentity getExperienceCloudId:^(NSString * _Nullable retrievedCloudId) {    
// handle the retrieved Id here    
}];
```

#### Swift {#swift-5}

```swift
ACPIdentity.getExperienceCloudId { (retrievedCloudId) in    
    // handle the retrieved Id here    
}
```

##   {#setadvertisingidentifier}
{% endtab %}
{% endtabs %}

## Set an Advertising Identifier

{% tabs %}
{% tab title="Android" %}
### setAdvertisingIdentifier

This API is part of the MobileCore extension. Adobe Identity extension supports the API, and sets the advertising identifier in the SDK.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

Remember the following information:

* If the Adobe Cloud Platform SDK is configured with `identity.adidEnabled` set to `false`, then the advertising identifier is not set or stored.
* If the current SDK privacy status is `optedout`, then the advertising identifier is not set.

### **Syntax** {#syntax-6}

```java
public static void setAdvertisingIdentifier(final String advertisingIdentifier);
```

### **Example** {#example-6}

```java
MobileCore.setAdvertisingIdentifier("advertising_identifier");
```
{% endtab %}

{% tab title="iOS" %}
### setAdvertisingIdentifier

This API is part of the ACPCore extension. Adobe Identity extension supports the API and sets the advertising identifier in the SDK.

If the IDFA was set in the SDK, the IDFA will be sent in lifecycle. It can also be accessed in Signals \(Postbacks\). This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

Remember the following information:

* If the Adobe Experience Cloud Platform SDKs is configured with `identity.adidEnabled` set to `false`, the advertising identifier is not set or stored.
* If the current SDK privacy status is `optedout`, the advertising identifier is not set.

### **Syntax** {#syntax-6}

```objectivec
+ (void) setAdvertisingIdentifier: (nullable NSString*) adId;
```

### **Examples** {#examples-6}

#### Objective-C {#objective-c-6}

```objectivec
[ACPCore setAdvertisingIdentifier:@"AdvertisingId"];
```

#### Swift {#swift-6}

```swift
ACPCore.setAdvertisingIdentifier("AdvertisingId")
```
{% endtab %}
{% endtabs %}

## Set the Push Identifier

{% tabs %}
{% tab title="Android" %}
### setPushIdentifier

This API is part of the MobileCore extension. Adobe Identity extension supports the API, and sets the device token for push notifications in the SDK. If the current SDK privacy status is `optedout`, the push identifier is not set.

### **Syntax** {#syntax-7}

```java
public static void setPushIdentifier(final String pushIdentifier);
```

### **Example** {#example-7}

```java
//Retrieve the token from either GCM or FCM, and pass it to the SDK
MobileCore.setPushIdentifier(token);
```
{% endtab %}

{% tab title="iOS" %}
### setPushIdentifier

This API is part of the ACPCore extension. Adobe Identity extension supports the API, and sets the device token for push notifications in the SDK. If the current SDK privacy status is `optedout`, the push identifier is not set.

### **Syntax** {#syntax-7}

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

### **Examples** {#examples-7}

#### Objective-C {#objective-c-7}

```objectivec
// Set the deviceToken that the APNS has assigned to the device
[ACPCore setPushIdentifier:deviceToken];
```

#### Swift {#swift-7}

```swift
// Set the deviceToken that the APNs has assigned to the device
ACPCore.setPushIdentifier(deviceToken)
```
{% endtab %}
{% endtabs %}

## Identity Service Classes

{% tabs %}
{% tab title="Android" %}
Here are the service classes for Identity in Android:

### AdobeCallback {#adobecallback}

This class provides the interface to receive results when the async APIs perform the requested action. For more information about these methods, see [Identity Service methods in Android](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/identity/identity-methods-in-android#identity-service-methods-in-android).

```java
public interface AdobeCallback<T> {    
    void call(final T value);
}
```

### VisitorID {#visitorid}

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

### AuthenticationState {#authenticationstate}

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

### ACPMobileVisitorAuthenticationState {#acpmobilevisitorauthenticationstate}

Used to indicate the authentication state for the current `VisitorID`.

```objectivec
typedef NS_ENUM(NSUInteger, 
    ADBMobileVisitorAuthenticationState) {    
    ACPMobileVisitorAuthenticationStateUnknown          = 0,    
    ACPMobileVisitorAuthenticationStateAuthenticated    = 1,    
    ACPMobileVisitorAuthenticationStateLoggedOut        = 2  };
```
{% endtab %}
{% endtabs %}

