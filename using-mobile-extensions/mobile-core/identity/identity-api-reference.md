# Identity API reference

## appendVisitorInfoForURL

{% tabs %}
{% tab title="Android" %}
This API appends Adobe visitor information to the query component of the specified URL.

If the provided URL is null or empty, it is returned as is. Otherwise, the following information is added to the query component of the specified URL and is returned in the [AdobeCallback](../mobile-core-api-reference.md#public-classes) instance:

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

When [AdobeCallbackWithError](../mobile-core-api-reference.md#public-classes) is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core-api-reference.md#public-classes).

#### Java

### appendVisitorInfoForURL

**Syntax**

```java
public static void appendVisitorInfoForURL(final String baseURL, final AdobeCallback<String> callback);
```

* _baseUrl_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
* _callback_ is invoked after the updated URL is available.

**Example**

```java
Identity.appendVisitorInfoForURL("https://example.com", new AdobeCallback<String>() {    
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
### appendToURL

This API appends Adobe visitor information to the query component of the specified URL.

If the provided URL is nil or empty, it is returned as is. Otherwise, the following information is added to the query component of the specified URL string and is returned via the callback:

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#gettrackingidentifier)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#setidentifier).

#### iOS

**Syntax**

```swift
static func appendTo(url: URL?, completion: @escaping (URL?, Error?) -> Void)
```

* _url_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
* _completion is invoked with \_urlWithVersionData_ after the updated URL is available or _error_ if an unexpected exception occurs or the request times out. The returned `Error` contains the [AEPError](../mobile-core-api-reference.md#public-classes) code of the specific error. The default timeout is 1000ms.

**Examples**

**Objective-C**

```objectivec
[AEPMobileIdentity appendToUrl:[NSURL URLWithString:@"https://example.com"] completion:^(NSURL * _Nullable url, NSError * error) {

  if (error) {
    // handle error here
  } else {
    // handle the appended url here
    if (urlWithVisitorData) {
      // APIs which update the UI must be called from main thread
      dispatch_async(dispatch_get_main_queue(), ^{
        [[self webView] loadRequest:[NSURLRequest requestWithURL:urlWithVisitorData]];
      }
    } else {
      // handle error, nil urlWithVisitorData
    }
  }
}];
```

**Swift**

```swift
Identity.appendTo(url: URL(string: "https://example.com")) { (appendedURL, error) in
    if let error = error {
    // handle error
  } else {
    // handle the appended url here
    if let appendedURL = appendedURL {
      // APIs which update the UI must be called from main thread
      DispatchQueue.main.async {
        self.webView.load(URLRequest(url: appendedURL!))
      }
    } else {
      // handle error, nil appendedURL
   }
}
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
{% endtabs %}

## extensionVersion

The `extensionVersion()` API returns the version of the Identity extension that is registered with the Mobile Core extension.

To get the version of the Identity extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
#### Java

```java
String identityExtensionVersion = Identity.extensionVersion();
```
{% endtab %}

{% tab title="iOS" %}
#### iOS

**Objective-C**

```objectivec
NSString *identityExtensionVersion = [AEPMobileIdentity extensionVersion];
```

**Swift**

```swift
var identityExtensionVersion  = AEPIdentity.extensionVersion
```
{% endtab %}
{% endtabs %}

## getExperienceCloudId

{% tabs %}
{% tab title="Android" %}
### getExperienceCloudId

This API retrieves the ECID that was generated when the app was initially launched and is stored in the ECID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. The values are returned via the [AdobeCallback](../mobile-core-api-reference.md#public-classes).

When [AdobeCallbackWithError](../mobile-core-api-reference.md#public-classes) is provided, and you are fetching the ECID from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core-api-reference.md#public-classes).

**Java**

**Syntax**

```java
public static void getExperienceCloudId(final AdobeCallback<String> callback);
```

* _callback_ is invoked after the ECID is available.

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

{% tab title="iOS" %}
### getExperienceCloudId

This API retrieves the ECID that was generated when the app was initially launched and is stored in the ECID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. The values are returned via the callback.

**Syntax**

```swift
@objc(getExperienceCloudId:)
static func getExperienceCloudId(completion: @escaping (String?, Error?) -> Void)
```

* completion is invoked after the ECID is available.  The default timeout is 1000ms.

**Examples**

**Objective-C**

```objectivec
[AEPMobileIdentity getExperienceCloudId:^(NSString * _Nullable exCloudId, NSError * error) {   
    // handle the retrieved ID here    
}];
```

**Swift**

```swift
Identity.getExperienceCloudId { (exCloudId, error) in
  if let error = error {
    // handle error here
  } else {
    // handle the retrieved ID here
  }
}
```
{% endtab %}
{% endtabs %}

## getIdentifiers

{% tabs %}
{% tab title="Android" %}
### getIdentifiers

This API returns all customer identifiers that were previously synced with the Adobe Experience Cloud through the [AdobeCallback](../mobile-core-api-reference.md#public-classes).

When [AdobeCallbackWithError](../mobile-core-api-reference.md#public-classes) is provided, and you are fetching the custom identifiers from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core-api-reference.md#public-classesr).

#### Java

**Syntax**

```java
public static void getIdentifiers(final AdobeCallback<List<VisitorID>> callback);
```

* _callback_ is invoked after the customer identifiers are available.

**Example**

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

This `getIdentifiers` API returns all customer identifiers that were previously synced with the Adobe Experience Cloud.

#### iOS

**Syntax**

```swift
@objc(getIdentifiers:)
static func getIdentifiers(completion: @escaping ([Identifiable]?, Error?) -> Void)
```

* _completion_ is invoked with _visitorIDs_ after the customer identifiers are available, or _error_ if an unexpected error occurs or the request times out. The returned `Error` contains the [AEPError](../mobile-core-api-reference.md#public-classes) code of the specific error. The default timeout is 1000ms.

**Examples**

**Objective-C**

```objectivec
[AEPMobileIdentity getIdentifiers:^(NSArray<id<AEPIdentifiable>> * _Nullable ids, NSError * error) {
  if (error) {
    // handle error here
  } else {
    // handle the retrieved identifiers here
  }
}];
```

**Swift**

```swift
Identity.getIdentifiers { (ids, error) in
  if let error = error {
    // handle error here
  } else {
    // handle the retrieved identifiers here
  }
}
```
{% endtab %}
{% endtabs %}

## getUrlVariables

{% tabs %}
{% tab title="Android" %}
### getUrlVariables

{% hint style="info" %}
This method was added in Core version 1.4.0 and Identity version 1.1.0_._
{% endhint %}

This API gets the Visitor ID Service variables in URL query parameter form, and these variables will be consumed by the hybrid app. This method returns an appropriately formed string that contains the Visitor ID Service URL variables. There will be no leading \(&\) or \(?\) punctuation because the caller is responsible for placing the variables in their resulting java.net.URI in the correct location.

If an error occurs while retrieving the URL string, _callback_ will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback as an [AdobeCallback](../mobile-core-api-reference.md#public-classes) instance:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

When [AdobeCallbackWithError](../mobile-core-api-reference.md#public-classes) is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core-api-reference.md#public-classes).

#### Java

**Syntax**

```java
public static void getUrlVariables(final AdobeCallback<String> callback);
```

* _callback_ has an NSString value that contains the visitor identifiers as a querystring after the service request is complete.

**Example**

```java
Identity.getUrlVariables(new AdobeCallback<String>() {    
    @Override    
    public void call(String stringWithAdobeVisitorInfo) {        
        //handle the URL query parameter string here 
        //For example, open the URL on the device browser        
        //        
        Intent i = new Intent(Intent.ACTION_VIEW);        
        i.setData(Uri.parse("https://example.com?" + urlWithAdobeVisitorInfo));        
        startActivity(i);    
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### getUrlVariables

This API gets the Visitor ID Service variables in URL query parameter form, and these variables will be consumed by the hybrid app. This method returns an appropriately formed string that contains the Visitor ID Service URL variables. There will be no leading \(&\) or \(?\) punctuation because the caller is responsible for placing the variables in their resulting java.net.URI in the correct location.

If an error occurs while retrieving the URL string, _callback_ will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

#### iOS

**Syntax**

```swift
@objc(getUrlVariables:)
static func getUrlVariables(completion: @escaping (String?, Error?) -> Void)
```

* _completion is invoked with \_urlVariables_ containing the visitor identifiers as a query string, or _error_ if an unexpected error occurs or the request times out. The returned Error\` contains the [AEPError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#acperror) code of the specific error. The default timeout is 500ms.

**Examples**

**Objective-C**

```objectivec
[AEPMobileIdentity getUrlVariables:^(NSString * _Nullable urlVariables, NSError * error) {
  if (error) {
    // handle error here
  } else {
    // handle the URL query parameter string here
    NSString* urlString = @"https://example.com";
    NSString* urlStringWithVisitorData = [NSString stringWithFormat:@"%@?%@", urlString, urlVariables];
    NSURL* urlWithVisitorData = [NSURL URLWithString:urlStringWithVisitorData];
    // APIs which update the UI must be called from main thread
    dispatch_async(dispatch_get_main_queue(), ^{
      [[self webView] loadRequest:[NSURLRequest requestWithURL:urlWithVisitorData]];
    }
  }
}];
```

**Swift**

```swift
Identity.getUrlVariables { (urlVariables, error) in
  if let error = error {
    // handle error
  } else {
    var urlStringWithVisitorData: String = "https://example.com"
    if let urlVariables: String = urlVariables {
      urlStringWithVisitorData.append("?" + urlVariables)
    }

    guard let urlWithVisitorData: URL = URL(string: urlStringWithVisitorData) else {
      // handle error, unable to construct URL
      return
    }
    // APIs which update the UI must be called from main thread
    DispatchQueue.main.async {
      self.webView.load(URLRequest(url: urlWithVisitorData))
    }
  }
}
```
{% endtab %}
{% endtabs %}

## registerExtension

The `registerExtension()` API registers the Identity extension with the Mobile Core extension. This API allows the extension to send and receive events to and from the Mobile SDK.

To register the Identity extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
After calling the `setApplication()` method in the `onCreate()` method, register the extension. If the registration was not successful, an `InvalidInitException` is thrown.

#### Java

```java
public class MobileApp extends Application {
@Override
public void onCreate() {
super.onCreate();
     MobileCore.setApplication(this);
     try {
         Identity.registerExtension();
     } catch (Exception e) {
         //Log the exception
     }
  }
}
```
{% endtab %}

{% tab title="iOS" %}
#### iOS

Use the `MobileCore.registerExtensions` API.
{% endtab %}
{% endtabs %}

## syncIdentifier

The `syncIdentifier()` and `syncIdentifiers()` APIs update the specified customer IDs with the Adobe Experience Cloud ID \(ECID\) Service.

These APIs synchronize the provided customer identifier type key and value with the authentication state to the ECID Service. If the specified customer ID type exists in the service, this ID type is updated with the new ID and the authentication state. Otherwise, a new customer ID is added.

Starting with _AEPIdentity v3.0.0 \(iOS\)_ and _Identity v1.1.2 \(Android\)_ if the new `identifier` value is null or empty, this ID type is removed from the local storage, Identity shared state and not synced with the Adobe ECID Service.

These IDs are preserved between app upgrades, are saved and restored during the standard application backup process, and are removed at uninstall.

If the current SDK privacy status is `MobilePrivacyStatus.OPT_OUT`, calling this method results in no operations being performed.

This API updates or appends the provided customer identifier type key and value with the given authentication state to the ECID Service. If the specified customer ID type exists in the service, the ID is updated with the new ID and authentication state. Otherwise a new customer ID is added.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static void syncIdentifier(final String identifierType,
                                      final String identifier,
                                      final VisitorID.AuthenticationState authenticationState);
```

* _identifierType \(String\)_ contains`the identifier type`, and this parameter should not be null or empty.
* _identifier \(String\)_ contains the `identifier value`, and this parameter should not be null or empty.
* _authenticationState_ indicates the authentication state of the user and contains one of the `VisitorID.AuthenticationState` values:
  * `VisitorID.AuthenticationState.AUTHENTICATED`
  * `VisitorID.AuthenticationState.LOGGED_OUT`
  * `VisitorID.AuthenticationState.UNKNOWN`

**Example**

```java
Identity.syncIdentifier("idType", 
                        "idValue", 
                        VisitorID.AuthenticationState.AUTHENTICATED);
```
{% endtab %}

{% tab title="iOS" %}
#### iOS

**Syntax**

```swift
@objc(syncIdentifierWithType:identifier:authenticationState:)
    static func syncIdentifier(identifierType: String, identifier: String, authenticationState: MobileVisitorAuthenticationState)
```

* The _identifierType \(String\)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier \(String\)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifier type` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* The value indicates the authentication state for the user and contains one of the following `MobileVisitorAuthenticationState` values:
  * `.authenticated`
  * `.loggedOut`
  * `.unknown`

**Examples**

**Objective-C**

```objectivec
[AEPMobileIdentity syncIdentifierWithType:@"id-type" identifier:@"id" authenticationState:AEPMobileVisitorAuthStateAuthenticated];
```

**Swift**

```swift
Identity.syncIdentifier(identifierType: "id-type", identifier: "id", authenticationState: .authenticated)
```
{% endtab %}
{% endtabs %}

## syncIdentifiers

This API is an overloaded version, which does not include the parameter for the authentication state and it assumes a default value of `VisitorID.AuthenticationState.UNKNOWN`.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers);
```

* _identifiers_ is a map that contains the identifiers with the Identifier type as the key, and the string identifier as the value.

  In each identifier pair, if the `identifier type` contains a null or an empty string, the identifier is ignored by the Identity extension.

**Example**

```java
Map<String, String> identifiers = new HashMap<String, String>();
identifiers.put("idType1", "idValue1");
identifiers.put("idType2", "idValue2");
identifiers.put("idType3", "idValue3");
Identity.syncIdentifier(identifiers);
```
{% endtab %}

{% tab title="iOS" %}
### iOS

**Syntax**

```swift
@objc(syncIdentifiers:)
    static func syncIdentifiers(identifiers: [String: String]?)
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

**Examples**

**Objective-C**

```objectivec
NSDictionary *identifiers = @{@"idType1":@"idValue1", 
                      @"idType2":@"idValue2", 
                      @"idType3":@"idValue3"};
[AEPMobileIdentity syncIdentifiers:identifiers];
```

**Swift**

```swift
let identifiers : [String: String] = ["idType1":"idValue1",
                                      "idType2":"idValue2",
                                      "idType3":"idValue3"];
Identity.syncIdentifiers(identifiers: identifiers)
```
{% endtab %}
{% endtabs %}

## syncIdentifiers \(overloaded\)

The function of this API is the same as the `syncIdentifier` API. This API passes a list of identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value. In each identifier pair, if the `identifier type` contains a null or an empty string, the identifier is ignored by the Identity extension.

Starting with _AEPIdentity v3.0.0 and \_Identity v1.1.2 \(Android\)_ if the new `identifier` value is null or empty, this ID type is removed from the local storage, Identity shared state and not synced with the Adobe ECID Service.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers, final VisitorID.AuthenticationState authState)
```

* _identifiers_ ia a map that contains IDs with the identifier type as the key, and the string identifier as the value.
* _authState_ indicates the authentication state for the user, which contains one of the following `VisitorID.AuthenticationState` values:
  * `VisitorID.AuthenticationState.AUTHENTICATED`
  * `VisitorID.AuthenticationState.LOGGED_OUT`
  * `VisitorID.AuthenticationState.UNKNOWN`

**Example**

```java
Map<String, String> identifiers = new HashMap<String, String>();
identifiers.put("idType1", "idValue1");
identifiers.put("idType2", "idValue2");
identifiers.put("idType3", "idValue3");
Identity.syncIdentifier(identifiers, VisitorID.AuthenticationState.AUTHENTICATED);
```
{% endtab %}

{% tab title="iOS" %}
#### iOS

**Syntax**

```swift
 @objc(syncIdentifiers:authenticationState:)
    static func syncIdentifiers(identifiers: [String: String]?, authenticationState: MobileVisitorAuthenticationState)
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

* The _authenticationState \(VisitorIDAuthenticationState\)_ indicates the authentication state of the user and contains one of the `VisitorID.AuthenticationState` values:
  * `VisitorID.AuthenticationState.AUTHENTICATED`
  * `VisitorID.AuthenticationState.LOGGED_OUT`
  * `VisitorID.AuthenticationState.UNKNOWN`

**Examples**

**Objective-C**

```objectivec
NSDictionary *identifiers = @{@"idType1":@"idValue1", 
                      @"idType2":@"idValue2", 
                      @"idType3":@"idValue3"};
[AEPMobileIdentity syncIdentifiers:identifiers authenticationState:AEPMobileVisitorAuthStateAuthenticated];
```

**Swift**

```swift
let identifiers : [String: String] = ["idType1":"idValue1",
                                      "idType2":"idValue2",
                                      "idType3":"idValue3"];
Identity.syncIdentifiers(identifiers: identifiers, authenticationState: .authenticated)
```
{% endtab %}
{% endtabs %}

## Public classes

{% tabs %}
{% tab title="Android" %}
#### Android

**AuthenticationState**

This class is used to indicate the authentication state for the current `VisitorID`.

```java
public enum AuthenticationState {        
       UNKNOWN,        
       AUTHENTICATED,        
       LOGGED_OUT;
}
```

**VisitorID**

This class is an identifier to be used with the Experience Cloud Visitor ID Service.

```java
public class VisitorID {    
     //Constructor    
     public VisitorID(String idOrigin, String idType, String id, VisitorID.AuthenticationState authenticationState);

     public VisitorID.AuthenticationState getAuthenticationState();   

     public final String getId();  

     public final String getIdOrigin();  

     public final String getIdType();

}
```
{% endtab %}

{% tab title="iOS" %}
#### iOS

**MobileVisitorAuthenticationState**

This is used to indicate the authentication state for the current `VisitorID`.

```objectivec
@objc(AEPMobileVisitorAuthState) public enum MobileVisitorAuthenticationState: Int, Codable {
    case unknown = 0
    case authenticated = 1
    case loggedOut = 2
}
```

**Identifiable**

This is an identifier to be used with the Experience Cloud Visitor ID Service and it contains the origin, the identifier type, the identifier and the authentication state of the visitor ID.

```swift
@objc(AEPIdentifiable) public protocol Identifiable {
    /// Origin of the identifier
    var origin: String? { get }

    /// Type of the identifier
    var type: String? { get }

    /// The identifier
    var identifier: String? { get }

    /// The authentication state for the identifier
    var authenticationState: MobileVisitorAuthenticationState { get }
}
```
{% endtab %}
{% endtabs %}

