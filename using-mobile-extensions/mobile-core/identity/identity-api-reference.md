# Identity API reference

## Sync identifiers<a id="syncIdentifiersTitle"></a>

The  `syncIdentifier()` and `syncIdentifiers()` APIs update the specified customer IDs  with the Adobe Experience Cloud ID service. 

These synchronize the provided customer identifier type key and value with the authentication state to the Adobe Experience Cloud ID Service. If the specified customer ID type exists in the service, this ID type is updated with the new ID and the authentication state. Otherwise, a new customer ID is added.

These IDs are  preserved between app upgrades, are saved and restored during the standard application backup process, and are removed at uninstall. 

If the current SDK privacy status  is `MobilePrivacyStatus.OPT_OUT`, calling this method results in no operations being performed.

{% tabs %}
{% tab title="Android" %}

### syncIdentifier<a id="syncIdentifier-java"></a>

This `syncIdentifier()` API updates or appends the provided customer identifier type key and value with the given authentication state to the Adobe Experience Cloud ID Service. If the given customer ID type already exists in the service, then it is updated with the new ID and authentication state. Otherwise a new customer ID is added.

#### **Syntax**

```text
public static void syncIdentifier(final String identifierType,
                                      final String identifier,
                                      final VisitorID.AuthenticationState authenticationState);
```

o  *identifierType* (String) containing identifier type, and the *identifier* (String) containing identifier value; should not be null or empty. If the identifierTtype and identifier do not have valid string values \(non null or empty\), that identifier is ignored by the Identity extension.

o  *authenticationState* indicates the authentication state of the user, which contains one of the VisitorID.AuthenticationState values `VisitorID.AuthenticationState.AUTHENTICATED`, `VisitorID.AuthenticationState.LOGGED_OUT`, `VisitorID.AuthenticationState.UNKNOWN`

#### **Example**

```java
Identity.syncIdentifier("idType", 
                        "idValue", 
                        VisitorID.AuthenticationState.AUTHENTICATED);
```

### syncIdentifiers<a id="syncIdentifiers-java"></a>

The function of the `syncIdentifiers`  API is same as the `syncIdentifier` API, which passes a list of identifiers each containing an identifier type as the key and an identifier as the value. In each of the identifiers pair, both identifier type and identifier should be non empty and non null values, otherwise they will be ignore. 

#### **Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers,
                                   final VisitorID.AuthenticationState authState)
```

o  *identifiers* map contains IDs with the Identifier type as the key, and the string identifier as the value. If the identifier type and identifier do not have valid string values \(non null or empty\), that identifier is ignored by the Identity extension.

o  *authState* indicates the authentication state for the user, which contains one of the VisitorID.AuthenticationState values `VisitorID.AuthenticationState.AUTHENTICATED`, `VisitorID.AuthenticationState.LOGGED_OUT`, `VisitorID.AuthenticationState.UNKNOWN`

#### Example

```java
Map<String, String> identifiers = new HashMap<String, String>();
identifiers.put("idType1", "idValue1");
identifiers.put("idType2", "idValue2");
identifiers.put("idType3", "idValue3");
Identity.syncIdentifier(identifiers, VisitorID.AuthenticationState.AUTHENTICATED);
```

### syncIdentifiers \(overloaded\)

This  API  `syncIdentifiers()` is an overloaded version that does not include the parameter for the Authentication State, and assumes a default value of `VisitorID.AuthenticationState.UNKNOWN`

These IDs are preserved between app upgrades, are saved and restored during the standard application backup process, and are removed at uninstall. 

#### **Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers);
```

o  *identifiers* is a map that contains the Identifiers with the Identifier type as the key, and the string identifier as the value. If the identifier type and identifier do not have valid string values \(non null or empty\), the identifier is ignored by the Identity extension.

#### Example

```java
Map<String, String> identifiers = new HashMap<String, String>();
identifiers.put("idType1", "idValue1");
identifiers.put("idType2", "idValue2");
identifiers.put("idType3", "idValue3");
Identity.syncIdentifier(identifiers);
```
{% endtab %}

{% tab title="iOS" %}

### syncIdentifier<a id="syncIdentifier-ios"></a>

This `syncIdentifier()` API updates or appends the provided customer identifier type key and value with the given authentication state to the Adobe Experience Cloud ID Service. If the given customer ID type already exists in the service, then it is updated with the new ID and authentication state. Otherwise a new customer ID is added.

#### **Syntax**

```objectivec
+ (void) syncIdentifier: (nonnull NSString*) identifierType             
             identifier: (nonnull NSString*) identifier
         authentication: (ADBMobileVisitorAuthenticationState) authenticationState;
```

o  *identifierType* (String) containing identifier type, and the *identifier* (String) containing identifier value; should not be null or empty. If the identifierTtype and identifier do not have valid string values \(non null or empty\), the identifier is ignored by the Identity extension.

o *authenticationState* (VisitorIDAuthenticationState) value indicating authentication state for the user contaisn one of the VisitorID.AuthenticationState values `ACPMobileVisitorAuthenticationStateAuthenticated`,`ACPMobileVisitorAuthenticationStateLoggedOut` and `ACPMobileVisitorAuthenticationStateUnknown`

#### Examples

**Objective-C**

```objectivec
[ACPIdentity syncIdentifier:@"idType" identifier:@"idValue" authentication:ACPMobileVisitorAuthenticationStateUnknown];
```

**Swift**

```swift
ACPIdentity.syncIdentifier("idType", identifier: "idValue", authentication: ACPMobileVisitorAuthenticationState.unknown)
```

### syncIdentifiers<a id="syncIdentifiers-ios"></a>

The function of this `syncIdentifiers()`  API is same as the `syncIdentifier` API, which passes a list of identifiers as a dictionary each containing an identifier type as the key and an identifier as the value. In each of the identifiers pair, both identifier type and identifier should be non empty and non null values, otherwise they will be ignore. 

#### Syntax

```objectivec
+ (void) syncIdentifiers: (nullable NSDictionary*) identifiers          
         authentication: (ACPMobileVisitorAuthenticationState) authenticationState;
```

o   *identifiers* is a dictionary that contains IDs with the Identifier type as the key, and the string identifier as the value. If the identifier type and identifier do not have valid string values \(non null or empty\), the identifier is ignored by the Identity extension.

o   *authenticationState* (VisitorIDAuthenticationState) value indicating authentication state for the user contaisn one of the VisitorID.AuthenticationState values `ACPMobileVisitorAuthenticationStateAuthenticated`,`ACPMobileVisitorAuthenticationStateLoggedOut` and `ACPMobileVisitorAuthenticationStateUnknown`

#### Examples

**Objective-C**

```objectivec
NSDictionary *ids = @{@"idType1":@"idValue1", 
                      @"idType2":@"idValue2", 
                      @"idType3":@"idValue3"};
[ACPIdentity syncIdentifiers:ids authentication:ACPMobileVisitorAuthenticationStateAuthenticated];
```

**Swift**

```swift
let identifiers : [String: String] = ["idType1":"idValue1",
                                      "idType2":"idValue2",
                                      "idType3":"idValue3"];
ACPIdentity.syncIdentifiers(identifiers, authentication:
ACPMobileVisitorAuthenticationState.authenticated)
```

### syncIdentifiers \(overloaded\) 

This  API  `syncIdentifiers()` is an overloaded version that does not include the parameter for the Authentication State, and assumes a default value as `ACPMobileVisitorAuthenticationStateUnknown`

#### Syntax

```objectivec
+ (void) syncIdentifiers: (nullable NSDictionary*) identifiers;
```

o  *identifiers* contains a dictionary of Identifiers with the Identifier type as the key, and the string identifier as the value. If the identifier type and identifier do not have valid string values \(non null or empty\), the identifier is ignored by the Identity extension.

#### Examples

**Objective-C**

```objectivec
NSDictionary *ids = @{@"idType1":@"idValue1", 
                      @"idType2":@"idValue2", 
                      @"idType3":@"idValue3"};
[ACPIdentity syncIdentifiers:ids];
```

**Swift**

```swift
let identifiers : [String: String] = ["idType1":"idValue1",
                                      "idType2":"idValue2",
                                      "idType3":"idValue3"];
ACPIdentity.syncIdentifiers(identifiers)
```

{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### syncIdentifier<a id="syncIdentifier-js"></a>

This `syncIdentifier()` API updates or appends the provided customer identifier type key and value with the given authentication state to the Adobe Experience Cloud ID Service. If the given customer ID type already exists in the service, then it is updated with the new ID and authentication state. Otherwise a new customer ID is added.

#### Syntax

```jsx
ACPIdentity.syncIdentifier(identifierType: String, identifier: String, authenticationState: string)
```

o *identifierType* (String) containing identifier type, and the *identifier* (String) containing identifier value; should not be null or empty. If the identifierTtype and identifier do not have valid string values \(non null or empty\), the identifier is ignored by the Identity extension.

o  *authenticationState* (VisitorIDAuthenticationState) value indicating authentication state for the user contaisn one of the VisitorID.AuthenticationState values `ACPMobileVisitorAuthenticationState.AUTHENTICATED`,`ACPMobileVisitorAuthenticationState.LOGGED_OUT` and `ACPMobileVisitorAuthenticationState.UNKNOWN`

#### Example

```jsx
ACPIdentity.syncIdentifier(identifierType, identifier, ACPMobileVisitorAuthenticationState.AUTHENTICATED);
```

### syncIdentifiers<a id="syncIdentifiers-js"></a>

The function of this `syncIdentifiers()`  API is same as the `syncIdentifier` API, which passes a list of identifiers as a dictionary each containing an identifier type as the key and an identifier as the value. In each of the identifiers pair, both identifier type and identifier should be non empty and non null values, otherwise they will be ignore. 

#### **Syntax**

```jsx
ACPIdentity.syncIdentifiers: (nullable NSDictionary*) identifiers;
```

o   *identifiers* is a dictionary that contains Identifiers with the Identifier type as the key, and the string identifier as the value. If the identifier type and identifier do not have valid string values \(non null or empty\), the identifier is ignored by the Identity extension.

#### Example**

```jsx
ACPIdentity.syncIdentifiers({"id1": "identifier1"});
```

### syncIdentifiersWithAuthState<a id="syncIdentifiersWithAuthState-js"></a>

The function of this `syncIdentifiersWithAuthState()`  API is same as the `syncIdentifier` API, which  passes a list of identifiers as a dictionary and  the authenticationState. The identifiers dictionary contains identifiers; each containing an identifier type as the key and an identifier as the value. In each of the identifiers pair, both identifier type and identifier should be non empty and non null values, otherwise they will be ignore. 

#### Syntax

```jsx
ACPIdentity.syncIdentifiersWithAuthState((nullable NSDictionary*) identifiers, authenticationState: string);
```

o  *identifiers* is a dictionary that contains IDs with the Identifier type as the key, and the string identifier as the value. If the identifier type and identifier do not have valid string values \(non null or empty\), the identifier is ignored by the Identity extension.

o  *authenticationState* (VisitorIDAuthenticationState) value indicates authentication state for the user containing one of the VisitorID.AuthenticationState values `ACPMobileVisitorAuthenticationState.AUTHENTICATED`,`ACPMobileVisitorAuthenticationState.LOGGED_OUT` and `ACPMobileVisitorAuthenticationState.UNKNOWN`

#### Example

```jsx
import {ACPMobileVisitorAuthenticationState} from '@adobe/react-native-acpcore';

ACPIdentity.syncIdentifiersWithAuthState({"id1": "identifier1"}, ACPMobileVisitorAuthenticationState.UNKNOWN);
```

{% endtab %}
{% endtabs %}

## Append visitor data to a URL <a id="appendToUrlTitle"></a>

{% tabs %}
{% tab title="Android" %}

### appendVisitorInfoForURL <a id="appendToUrl-java"></a>

This `appendVisitorInfoForURL()` API appends Adobe visitor information to the query component of the given URL.

If the provided URL is null or empty, it is returned as is. Otherwise, the following information is added to the query component of the given URL and is returned in the [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback) instance:

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

#### **Syntax**

```java
public static void appendVisitorInfoForURL(final String baseURL, final AdobeCallback<String> callback);
```

o  *baseUrl* is the URL to which the visitor info needs to be appended. Returned as is if it is nil or empty.

o  *callback* is the method that is invoked after the updated URL is available.

#### Example**

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

{% hint style="info" %}
This API is designed to handle the following URL formats:

```text
scheme://authority/path?query=param#fragment
```

In this example, the Adobe visitor data is appended as:

```text
scheme://authority/path?query=param&TS=timestamp&MCMID=ecid&MCORGID=ecorgid@AdobeOrg#fragment
```

Similarly, URLs without a query component:

```text
scheme://authority/path#fragment
```

The Adobe visitor data is appended as:

```text
scheme://authority/path?TS=timestamp&MCMID=ecid&MCORGID=ecorgid@AdobeOrg#fragment
```

If your application uses more complicated URLs, such as Angular URLs, we recommend that you use [getUrlVariables](identity-api-reference.md#geturlvariables-java).
{% endhint %}
{% endtab %}

{% tab title="iOS" %}
### appendToURL <a id="appendToUrl-ios"></a>

This `appendToURL()` API appends Adobe visitor information to the query component of the given URL

If the provided URL is nil or empty, it is returned as is. Otherwise, the following information is added to the query component of the given URL string and is returned via the callback:

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](../../adobe-analytics/)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/174e9069bc1d3a521b59d52a066e9a7730f60ff5/using-mobile-extensions/adobe-analytics/analytics-api-reference/README.md#setidentifier).

#### **Syntax**

```objectivec
+ (void) appendToUrl: (nullable NSURL*) baseUrl withCallback: (nullable void (^) (NSURL* __nullable urlWithVisitorData)) callback;
```

*o baseUrl* is the URL to which the visitor info needs to be appended. Returned as is if it is nil or empty.

*o callback* is the method that is invoked after the updated URL is available.

#### Examples**

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

{% hint style="info" %}
This API is designed to handle the following URL formats:

```text
scheme://authority/path?query=param#fragment
```

In this example, the Adobe visitor data is appended as:

```text
scheme://authority/path?query=param&TS=timestamp&MCMID=ecid&MCORGID=ecorgid@AdobeOrg#fragment
```

Similarly, URLs without a query component:

```text
scheme://authority/path#fragment
```

The Adobe visitor data is appended as:

```text
scheme://authority/path?TS=timestamp&MCMID=ecid&MCORGID=ecorgid@AdobeOrg#fragment
```

If your application uses more complicated URLs, such as Angular URLs, we recommend that you use [getUrlVariables](identity-api-reference.md#geturlvariables-ios).
{% endhint %}
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### appendVisitorInfoForURL <a id="appendToUrl-js"></a>

This `appendVisitorInfoForURL()` API appends Adobe visitor information to the query component of the given URL.

If the given url is nil or empty, it is returned as is. Otherwise, the following information is added to the query component of the given URL.

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](../../adobe-analytics/)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/174e9069bc1d3a521b59d52a066e9a7730f60ff5/using-mobile-extensions/adobe-analytics/analytics-api-reference/README.md#setidentifier).

#### Syntax

```jsx
ACPIdentity.appendVisitorInfoForURL(baseURL);
```

o *baseUrl* is the URL to which the visitor info needs to be appended. Returned as is if it is nil or empty.

#### Example

```jsx
ACPIdentity.appendVisitorInfoForURL("www.myUrl.com").then(urlWithVistorData => console.log("AdobeExperenceSDK: Url with Visitor Data = " + urlWithVisitorData));
```

{% hint style="info" %}
This API is designed to handle the following URL formats:

```text
scheme://authority/path?query=param#fragment
```

In this example, the Adobe visitor data is appended as:

```text
scheme://authority/path?query=param&TS=timestamp&MCMID=ecid&MCORGID=ecorgid@AdobeOrg#fragment
```

Similarly, URLs without a query component:

```text
scheme://authority/path#fragment
```

The Adobe visitor data is appended as:

```text
scheme://authority/path?TS=timestamp&MCMID=ecid&MCORGID=ecorgid@AdobeOrg#fragment
```

If your application uses more complicated URLs, such as Angular URLs, we recommend that you use [getUrlVariables](identity-api-reference.md#geturlvariables-js).
{% endhint %}
{% endtab %}
{% endtabs %}

## Get visitor data as URL query parameter <a id="getUrlVariablesTitle"></a>

{% tabs %}
{% tab title="Android" %}
### getUrlVariables <a id="geturlvariables-java"></a>

{% hint style="info" %}
This method was added in Core version 1.4.0 and Identity version 1.1.0_._
{% endhint %}

This `getUrlVariables()` API gets the Visitor ID Service variables in URL query parameter form for consumption in hybrid app. This method will return an appropriately formed string containing Visitor ID Service URL variables. There will be no leading (&) or (?) punctuation, as the caller is responsible for placing it in their resulting java.net.URI in the correct location.

If an error occurs while retrieving the URL string, (*callback*) will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback as an [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback) instance:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

#### **Syntax**

```java
public static void getUrlVariables(final AdobeCallback<String> callback);
```

o   *callback* is a block pointer to call with an NSString value that contains the visitor identifiers as a querystring upon completion of the service request.

#### Example**

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
### getUrlVariables <a id="geturlvariables-ios"></a>

{% hint style="info" %}
This method was added in ACPCore version 2.3.0 and ACPIdentity version 2.1.0.
{% endhint %}

* This `getUrlVariables()` API gets the Visitor ID Service variables in URL query parameter form for consumption in hybrid app. This method will return an appropriately formed string containing Visitor ID Service URL variables. There will be no leading (&) or (?) punctuation, as the caller is responsible for placing it in their resulting java.net.URI in the correct location.

  If an error occurs while retrieving the URL string, (*callback*) will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback as an [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback) instance:

  - The `adobe_mc` attribute is an URL encoded list that contains:
    - `MCMID` - Experience Cloud ID \(ECID\)
    - `MCORGID` - Experience Cloud Org ID
    - `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
    - `TS` - A timestamp taken when this request was made
  - The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

#### **Syntax**

```objectivec
+ (void) getUrlVariables: (nonnull void (^) (NSString* __nullable urlVariables)) callback;
```

o   *callback* is a block pointer to call with an NSString value that contains the visitor identifiers as a querystring upon completion of the service request.

#### Examples

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

{% tab title="React Native" %}
#### JavaScript

### getUrlVariables <a id="geturlvariables-js"></a>

_{% hint style="info" %}
This method was added in react-native-acpcore v1.0.5.
{% endhint %}_

This `getUrlVariables()` API gets the Visitor ID Service variables in URL query parameter form for consumption in hybrid app. This method will return an appropriately formed string containing Visitor ID Service URL variables. There will be no leading (&) or (?) punctuation, as the caller is responsible for placing it in their resulting java.net.URI in the correct location.

If an error occurs while retrieving the URL string, (*callback*) will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback as an [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback) instance:

- The `adobe_mc` attribute is an URL encoded list that contains:
  - `MCMID` - Experience Cloud ID \(ECID\)
  - `MCORGID` - Experience Cloud Org ID
  - `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  - `TS` - A timestamp taken when this request was made
- The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

#### Syntax

```jsx
ACPIdentity.getUrlVariables();
```

#### Example

```jsx
ACPIdentity.getUrlVariables().then(urlVariables => console.log("AdobeExperenceSDK: query params = " + urlVariables));
```
{% endtab %}
{% endtabs %}

## Get identifiers<a id="getIdentifiersTitle"></a>

{% tabs %}
{% tab title="Android" %}
### getIdentifiers<a id="getIdentifiers-java"></a>

This `getIdentifiers()` API returns all customer identifiers that were previously synced with the Adobe Experience Cloud through the [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback).

#### **Syntax**

```java
public static void getIdentifiers(final AdobeCallback<List<VisitorID>> callback);
```

o   *callback* is a method which will be invoked once the customer identifiers are available.

#### Example

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
### getIdentifiers<a id="getIdentifiers-ios"></a>

This `getIdentifiers` API returns all customer identifiers that were previously synced with the Adobe Experience Cloud

#### **Syntax**

```objectivec
+ (void) getIdentifiers: (nonnull void (^) (NSArray<ADBMobileVisitorId*>* __nullable visitorIDs)) callback;
```

o  *callback* is a method which will be invoked once the customer identifiers are available.

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

### getIdentifiers<a id="getIdentifiers-js"></a>

This `getIdentifiers` API returns all customer identifiers that were previously synced with the Adobe Experience Cloud

#### Syntax

```jsx
ACPIdentity.getIdentifiers()
```

#### Example

```jsx
ACPIdentity.getIdentifiers().then(identifiers => console.log("AdobeExperienceSDK: Identifiers = " + identifiers));
```
{% endtab %}
{% endtabs %}

## Get Experience Cloud IDs<a id="getExperienceCloudIdTitle"></a>

{% tabs %}
{% tab title="Android" %}
### getExperienceCloudId<a id="getExperienceCloudId-java"></a>

This `getExperienceCloudId` API retrieves the Experience Cloud ID that was generated at initial launch  and stored in the Experience Cloud ID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. The values are returned via the [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback).

#### **Syntax**

```java
public static void getExperienceCloudId(final AdobeCallback<String> callback);
```

o  *callback* method  will be invoked once Experience Cloud ID is available

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
### getExperienceCloudId<a id="getExperienceCloudId-ios"></a>

This `getExperienceCloudId` API retrieves the Experience Cloud ID that was generated at initial launch  and stored in the Experience Cloud ID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. The values are returned via the [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#adobecallback).

#### **Syntax**

```objectivec
+ (void) getExperienceCloudId: (nonnull void (^) (NSString* __nullable experienceCloudId)) callback;
```

o  *callback* method  will be invoked once Experience Cloud ID is available

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

### getExperienceCloudId<a id="getExperienceCloudId-js"></a>

This `getExperienceCloudId` API retrieves the Experience Cloud ID that was generated at initial launch  and stored in the Experience Cloud ID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

#### Syntax

```jsx
ACPIdentity.getExperienceCloudId()
```

#### Example

```jsx
ACPIdentity.getExperienceCloudId().then(cloudId => console.log("AdobeExperienceSDK: CloudID = " + cloudId));
```
{% endtab %}
{% endtabs %}

## Set an advertising identifier<a id="setAdvertisingIdentifierTitle"></a>

The advertising ID is preserved between app upgrades, is saved and restored during the standard application backup process, available via [Signals](../signals/), and is removed at uninstall.

{% hint style="info" %}
If the current SDK privacy status is `optedout`, the advertising identifier is not set or stored.
{% endhint %}

{% tabs %}
{% tab title="Android" %}

### setAdvertisingIdentifier<a id="setAdvertisingIdentifier-java"></a>

This `setAdvertisingIdentifier()` API sets  the advertising identifier provided. 

#### **Syntax**

```java
public static void setAdvertisingIdentifier(final String advertisingIdentifier);
```

o *advertisingIdentifier* is a String that provides developers with a simple, standard system to continue to track the Ads through their apps	 

#### **Example**

{% hint style="warning" %}
This is just an implementation example. For more information about advertising identifiers and how to handle them correctly in your mobile application, see [Google Play Services documentation about Advertising ID](http://www.androiddocs.com/google/play-services/id.html).
{% endhint %}

This example requires Google Play Services to be configured in your mobile application. For instructions on how to import the Google Mobile Ads SDK and how to configure your ApplicationManifest.xml file, see [Google Mobile Ads SDK setup](https://developers.google.com/admob/android/quick-start#import_the_mobile_ads_sdk).

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
{% endtab %}

{% tab title="iOS" %}
### setAdvertisingIdentifier<a id="setAdvertisingIdentifier-ios"></a>

{% hint style="info" %}
Retrieve the Identifier for Advertising \(IDFA\) from Apple APIs only if you are using an ad service. If you retrieve IDFA, and are not using it properly, your app might be rejected.
{% endhint %}

{% hint style="warning" %}
This is just an implementation example. For more information about IDFA and how to handle them correctly in your mobile application, see [Apple developer documentation about IDFA](https://developer.apple.com/documentation/adsupport/asidentifiermanager)
{% endhint %}

#### **Syntax**

```objectivec
+ (void) setAdvertisingIdentifier: (nullable NSString*) adId;
```

o *adId* is a String that provides developers with a simple, standard system to continue to track the Ads through their apps	

#### **Example**

**Objective-C**

```objectivec
#import <AdSupport/ASIdentifierManager.h>
...

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString *idfa = nil;
    if ([[ASIdentifierManager sharedManager] isAdvertisingTrackingEnabled]) {
        idfa = [[[ASIdentifierManager sharedManager] advertisingIdentifier] UUIDString];
    } else {
        [ACPCore log:ACPMobileLogLevelDebug tag:@"AppDelegateExample" message:@"Advertising Tracking is disabled by the user, cannot process the advertising identifier"];
    }
    [ACPCore setAdvertisingIdentifier:idfa];
    ...
}
```

**Swift**

```swift
import AdSupport
...

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    var idfa:String = "";
    if (ASIdentifierManager.shared().isAdvertisingTrackingEnabled) {
        idfa = ASIdentifierManager.shared().advertisingIdentifier.uuidString;
    } else {
        ACPCore.log(ACPMobileLogLevel.debug, tag: "AppDelegateExample", message: "Advertising Tracking is disabled by the user, cannot process the advertising identifier");
    }
    ACPCore.setAdvertisingIdentifier(idfa);
    ...
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### setAdvertisingIdentifier<a id="setAdvertisingIdentifier-js"></a>

```jsx
ACPCore.setAdvertisingIdentifier("adID");
```
o *adID* is a String that provides developers with a simple, standard system to continue to track the Ads through their apps	

{% endtab %}
{% endtabs %}

## Set the push identifier<a id="setPushIdentifierTitle"></a>

This `setPushIdentifier` API sets the device token for push notifications in the SDK. If the current SDK privacy status is `optedout`, the push identifier is not set.

{% tabs %}
{% tab title="Android" %}
### setPushIdentifier<a id="setPushIdentifier-java"></a>

#### **Syntax**

```java
public static void setPushIdentifier(final String pushIdentifier);
```

o *pushIdentifier* is a String that contains the device token for push notifications.

#### **Example**

```java
//Retrieve the token from either GCM or FCM, and pass it to the SDK
MobileCore.setPushIdentifier(token);
```
{% endtab %}

{% tab title="iOS" %}
### setPushIdentifier<a id="setPushIdentifier-ios"></a>

#### **Objective-C**

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

o *deviceToken* is a String that contains the device token for push notifications.

#### Example

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

### setPushIdentifier<a id="setPushIdentifier-js"></a>

```jsx
ACPCore.setPushIdentifier("pushIdentifier");
```
o *pushIdentifier* is a String that contains the device token for push notifications.

{% endtab %}
{% endtabs %}

## Identity service classes

{% tabs %}
{% tab title="Android" %}

#### Android

### AdobeCallback <a id="adobecallback"></a>

This class provides the interface to receive results when the async APIs perform the requested action.

```java
public interface AdobeCallback<T> {    
    void call(final T value);
}
```

### VisitorID <a id="visitorid"></a>

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

### AuthenticationState <a id="authenticationstate"></a>

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

#### iOS

### ACPMobileVisitorId<a id="acpmobileVisitorId"></a>

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

### ACPMobileVisitorAuthenticationState <a id="acpmobilevisitorauthenticationstate"></a>

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

### ACPVisitorID<a id="acpvisitorid"></a>

```jsx
import {ACPVisitorID} from '@adobe/react-native-acpcore';

var visitorId = new ACPVisitorID(idOrigin?: string, idType: string, id?: string, authenticationState?: ACPMobileVisitorAuthenticationState)
```
{% endtab %}
{% endtabs %}

