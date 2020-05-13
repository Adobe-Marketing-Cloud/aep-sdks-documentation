# Identity API reference

## appendVisitorInfoForURL

{% tabs %}
{% tab title="Android" %}
This API appends Adobe visitor information to the query component of the specified URL.

If the provided URL is null or empty, it is returned as is. Otherwise, the following information is added to the query component of the specified URL and is returned in the [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobecallback) instance:

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

When [AdobeCallbackWithError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobecallbackwitherror) is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate \[AdobeError\][https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference\#adobeerror](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobeerror)\).

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

{% hint style="info" %}
Method `appendToUrl:withCompletionHandler` was added in ACPCore version 2.5.0 and ACPIdentity version 2.2.0.
{% endhint %}

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

```objectivec
+ (void) appendToUrl: (nullable NSURL*) baseUrl withCallback: (nullable void (^) (NSURL* __nullable urlWithVisitorData)) callback;
+ (void) appendToUrl: (nullable NSURL*) baseUrl withCompletionHandler: (nullable void (^) (NSURL* __nullable urlWithVersionData, NSError* __nullable error)) completionHandler;
```

* _baseUrl_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
* _callback_ is invoked after the updated URL is available.
* _completionHandler_ is invoked with _urlWithVersionData_ after the updated URL is available or _error_ if an unexpected exception occurs or the request times out. The returned `NSError` contains the [ACPError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#acperror) code of the specific error. The default timeout is 500ms.

**Examples**

**Objective-C**

```objectivec
NSURL* url = [[NSURL alloc] initWithString:@"https://example.com"];
[ACPIdentity appendToUrl:url withCallback:^(NSURL * _Nullable urlWithVisitorData) {    
  // handle the appended url here
  if (urlWithVisitorData) {
    // APIs which update the UI must be called from main thread
    dispatch_async(dispatch_get_main_queue(), ^{
      [[self webView] loadRequest:[NSURLRequest requestWithURL:urlWithVisitorData]];
    }
  } else {
    // handle error, nil urlWithVisitorData
  }
}];

[ACPIdentity appendToUrl:url withCompletionHandler:^(NSURL * _Nullable urlWithVersionData, NSError * _Nullable error) {
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
ACPIdentity.append(to:URL(string: "https://example.com"), withCallback: {(appendedURL) in    
  // handle the appended url here
  if let appendedURL = appendedURL {
    // APIs which update the UI must be called from main thread
    DispatchQueue.main.async {
      self.webView.load(URLRequest(url: appendedURL!))
    }
  } else {
    // handle error, nil appendedURL
  }
});

ACPIdentity.append(to: URL(string: "https://example.com"), withCompletionHandler: { (appendedURL, error) in
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
})
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
### appendVisitorInfoForURL

This API appends Adobe visitor information to the query component of the specified URL.

If the specified URL is nil or empty, it is returned as is. Otherwise, the following information is added to the query component of the specified URL.

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#gettrackingidentifier)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#setidentifier).

#### JavaScript

**Syntax**

```jsx
appendVisitorInfoForURL(baseURL?: String): Promise<?string>;
```

* _baseUrl_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.

**Example**

```jsx
ACPIdentity.appendVisitorInfoForURL("https://example.com").then(urlWithVistorData => console.log("AdobeExperenceSDK: Url with Visitor Data = " + urlWithVisitorData));
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

{% tab title="Flutter" %}
### appendVisitorInfoForURL

This API appends Adobe visitor information to the query component of the specified URL.

If the specified URL is nil or empty, it is returned as is. Otherwise, the following information is added to the query component of the specified URL.

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#gettrackingidentifier)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#setidentifier).

#### Dart

**Syntax**

```dart
Future<String> appendToUrl (String url);
```

* _url_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.

**Example**

```dart
String result = "";

try {
  result = await FlutterACPIdentity.appendToUrl("https://example.com");
} on PlatformException {
  log("Failed to append URL");
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

If your application uses more complicated URLs, such as Angular URLs, we recommend that you use getUrlVariables.
{% endhint %}
{% endtab %}

{% tab title="Cordova" %}
### appendVisitorInfoForURL

This API appends Adobe visitor information to the query component of the specified URL.

If the specified URL is nil or empty, it is returned as is. Otherwise, the following information is added to the query component of the specified URL.

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#gettrackingidentifier)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#setidentifier).

#### Cordova

**Syntax**

```jsx
ACPIdentity.appendVisitorInfoForUrl = function(url, success, fail);
```

* _url_ _\(String\)_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
* _success_ is a callback containing the provided URL with the visitor information appended if the `appendVisitorInfoForUrl` API executed without any errors.
* _fail_ is a callback containing error information if the  `appendVisitorInfoForUrl` API was executed with errors.

**Example**

```jsx
ACPIdentity.appendVisitorInfoForUrl("https://example.com", function(handleCallback) {
  console.log("AdobeExperenceSDK: Url with Visitor Data = " + handleCallback);
}, function(handleError) {
  console.log("AdobeExperenceSDK: Failed to append URL : " + handleError);
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

If your application uses more complicated URLs we recommend that you use [getUrlVariables](identity-api-reference.md#geturlvariables-cordova).
{% endhint %}
{% endtab %}

{% tab title="Unity" %}
### AppendToUrl

This API appends Adobe visitor information to the query component of the specified URL.

If the specified URL is nil or empty, it is returned as is. Otherwise, the following information is added to the query component of the specified URL.

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#gettrackingidentifier)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#setidentifier).

#### C\#

**Syntax**

```csharp
public static void AppendToUrl(string url, AdobeIdentityAppendToUrlCallback callback)
```

* _url_ _\(String\)_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
* _callback_ is a callback containing the provided URL with the visitor information appended if the `AppendToUrl` API executed without any errors.

**Example**

```csharp
[MonoPInvokeCallback(typeof(AdobeIdentityAppendToUrlCallback))]
public static void HandleAdobeIdentityAppendToUrlCallback(string url)
{
    print("Url is : " + url);
}
ACPIdentity.AppendToUrl("https://www.adobe.com", HandleAdobeIdentityAppendToUrlCallback);
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

If your application uses more complicated URLs we recommend that you use [getUrlVariables](identity-api-reference.md#geturlvariables-cordova).
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
NSString *identityExtensionVersion = [ACPIdentity extensionVersion];
```

**Swift**

```swift
var identityExtensionVersion  = ACPIdentity.extensionVersion()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```jsx
ACPIdentity.extensionVersion().then(identityExtensionVersion => console.log("AdobeExperienceSDK: ACPIdentity version: " + identityExtensionVersion));
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

```dart
String identityExtensionVersion = FlutterACPIdentity.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

**Syntax**

```jsx
ACPIdentity.extensionVersion = function(success, fail);
```

* _success_ is a callback containing the ACPIdentity extension version if the `extensionVersion` API executed without any errors.
* _fail_ is a callback containing error information if the  `appendVisitorInfoForUrl` API was executed with errors.

**Example**

```jsx
ACPIdentity.extensionVersion(function (handleCallback) {
  console.log("AdobeExperienceSDK: ACPIdentity version: " + handleCallback)
}, function (handleError) {
  console.log("AdobeExperenceSDK: failed to get extension version : " + handleError)
});
```
{% endtab %}

{% tab title="Unity" %}
#### C\#

**Syntax**

```csharp
public static string ExtensionVersion()
```

**Example**

```csharp
string identityVersion = ACPIdentity.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

## getExperienceCloudId

{% tabs %}
{% tab title="Android" %}
### getExperienceCloudId

This API retrieves the ECID that was generated when the app was initially launched and is stored in the ECID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. The values are returned via the \[AdobeCallback\][https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference\#adobecallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobecallback)\).

When [AdobeCallbackWithError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobecallbackwitherror) is provided, and you are fetching the ECID from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobeerror).

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

{% hint style="info" %}
Method `getExperienceCloudIdWithCompletionHandler` was added in ACPCore version 2.5.0 and ACPIdentity version 2.2.0.
{% endhint %}

This API retrieves the ECID that was generated when the app was initially launched and is stored in the ECID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. The values are returned via the callback.

**Syntax**

```objectivec
+ (void) getExperienceCloudId: (nonnull void (^) (NSString* __nullable experienceCloudId)) callback;
+ (void) getExperienceCloudIdWithCompletionHandler: (nonnull void (^) (NSString* __nullable experienceCloudId, NSError* __nullable error)) completionHandler;
```

* _callback_ is invoked after the ECID is available.
* _completionHandler_ is invoked with _experienceCloudId_ after the ECID is available, or _error_ if an unexpected error occurs or the request times out. The returned `NSError` contains the [ACPError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#acperror) code of the specific error. The default timeout is 500ms.

**Examples**

**Objective-C**

```objectivec
[ACPIdentity getExperienceCloudId:^(NSString * _Nullable retrievedCloudId) {    
    // handle the retrieved ID here    
}];

[ACPIdentity getExperienceCloudIdWithCompletionHandler:^(NSString * _Nullable experienceCloudId, NSError * _Nullable error) {
  if (error) {
    // handle error here
  } else {
    // handle the retrieved ID here
  }
}];
```

**Swift**

```swift
ACPIdentity.getExperienceCloudId { (retrievedCloudId) in    
    // handle the retrieved ID here    
}

ACPIdentity.getExperienceCloudId { (retrievedCloudId, error) in
  if let error = error {
    // handle error here
  } else {
    // handle the retrieved ID here
  }
}
```
{% endtab %}

{% tab title="React Native" %}
### getExperienceCloudId

This API retrieves the ECID that was generated when the app was initially launched and is stored in the ECID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

#### JavaScript

#### Syntax

```jsx
getExperienceCloudId(): Promise<?string>;
```

#### Example

```jsx
ACPIdentity.getExperienceCloudId().then(cloudId => console.log("AdobeExperienceSDK: CloudID = " + cloudId));
```
{% endtab %}

{% tab title="Flutter" %}
### getExperienceCloudId

This API retrieves the ECID that was generated when the app was initially launched and is stored in the ECID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

#### Dart

#### Syntax

```dart
Future<String> experienceCloudId;
```

#### Example

```dart
String result = "";

try {
  result = await FlutterACPIdentity.experienceCloudId;
} on PlatformException {
  log("Failed to get experienceCloudId");
}
```
{% endtab %}

{% tab title="Cordova" %}
### getExperienceCloudId

This API retrieves the ECID that was generated when the app was initially launched and is stored in the ECID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

#### Cordova

#### Syntax

```jsx
ACPIdentity.getExperienceCloudId(success, fail);
```

* _success_ is a callback containing the experience cloud id if the `getExperienceCloudId` API executed without any errors.
* _fail_ is a callback containing error information if the `getExperienceCloudId` API was executed with errors.

#### Example

```jsx
ACPIdentity.getExperienceCloudId(function (handleCallback) {
  console.log("AdobeExperienceSDK: experienceCloudId: " + handleCallback)
}, function (handleError) {
  console.log("AdobeExperenceSDK: Failed to retrieve experienceCloudId : " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
### getExperienceCloudId

This API retrieves the ECID that was generated when the app was initially launched and is stored in the ECID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

#### C\#

#### Syntax

```csharp
public static void GetExperienceCloudId(AdobeGetExperienceCloudIdCallback callback)
```

* _callback_ is a callback containing the experience cloud id if the `getExperienceCloudId` API executed without any errors.

#### Example

```csharp
[MonoPInvokeCallback(typeof(AdobeGetExperienceCloudIdCallback))]
public static void HandleAdobeGetExperienceCloudIdCallback(string cloudId)
{
    print("ECID is : " + cloudId);
}
ACPIdentity.GetExperienceCloudId(HandleAdobeGetExperienceCloudIdCallback);
```
{% endtab %}
{% endtabs %}

## getIdentifiers

{% tabs %}
{% tab title="Android" %}
### getIdentifiers

This API returns all customer identifiers that were previously synced with the Adobe Experience Cloud through the [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobecallback).

When [AdobeCallbackWithError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobecallbackwitherror) is provided, and you are fetching the custom identifiers from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobeerror).

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

{% hint style="info" %}
Method `getIdentifiersWithCompletionHandler` was added in ACPCore version 2.5.0 and ACPIdentity version 2.2.0.
{% endhint %}

This `getIdentifiers` API returns all customer identifiers that were previously synced with the Adobe Experience Cloud.

#### iOS

**Syntax**

```objectivec
+ (void) getIdentifiers: (nonnull void (^) (NSArray<ADBMobileVisitorId*>* __nullable visitorIDs)) callback;
+ (void) getIdentifiersWithCompletionHandler: (nonnull void (^) (NSArray<ACPMobileVisitorId*>* __nullable visitorIDs, NSError* __nullable error)) completionHandler;
```

* _callback_ is invoked after the customer identifiers are available.
* _completionHandler_ is invoked with _visitorIDs_ after the customer identifiers are available, or _error_ if an unexpected error occurs or the request times out. The returned `NSError` contains the [ACPError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#acperror) code of the specific error. The default timeout is 500ms.

**Examples**

**Objective-C**

```objectivec
[ACPIdentity getIdentifiers:^(NSArray<ACPMobileVisitorId *> * _Nullable retrievedVisitorIds) {    
    // handle the retrieved identifiers here     
}];

[ACPIdentity getIdentifiersWithCompletionHandler:^(NSArray<ACPMobileVisitorId *> * _Nullable visitorIDs, NSError * _Nullable error) {
  if (error) {
    // handle error here
  } else {
    // handle the retrieved identifiers here
  }
}];
```

**Swift**

```swift
ACPIdentity.getIdentifiers { (retrievedVisitorIds) in    
   // handle the retrieved identifiers here        
}

ACPIdentity.getIdentifiersWithCompletionHandler { (retrievedVisitorIds, error) in
  if let error = error {
    // handle error here
  } else {
    // handle the retrieved identifiers here
  }
}
```
{% endtab %}

{% tab title="React Native" %}
### getIdentifiers

This API returns all customer identifiers that were previously synced with the Adobe Experience Cloud.

#### JavaScript

**Syntax**

```jsx
getIdentifiers(): Promise<Array<?ACPVisitorID>>;
```

**Example**

```jsx
ACPIdentity.getIdentifiers().then(identifiers => console.log("AdobeExperienceSDK: Identifiers = " + identifiers));
```
{% endtab %}

{% tab title="Flutter" %}
### getIdentifiers

This API returns all customer identifiers that were previously synced with the Adobe Experience Cloud.

#### Dart

**Syntax**

```dart
 Future<List<ACPMobileVisitorId>> identifiers;
```

**Example**

```dart
List<ACPMobileVisitorId> result;

try {
  result = await FlutterACPIdentity.identifiers;
} on PlatformException {
  log("Failed to get identifiers");
}
```
{% endtab %}

{% tab title="Cordova" %}
### getIdentifiers

This API returns all customer identifiers that were previously synced with the Adobe Experience Cloud.

#### Cordova

**Syntax**

```jsx
ACPIdentity.getIdentifiers(success, fail);
```

* _success_ is a callback containing the previously synced identifiers if the `getIdentifiers` API executed without any errors.
* _fail_ is a callback containing error information if the `getIdentifiers` API was executed with errors.

**Example**

```jsx
ACPIdentity.getIdentifiers(function (handleCallback) {
  console.log("AdobeExperienceSDK: Visitor identifiers: " + handleCallback);
}, function (handleError) {
  console.log("AdobeExperenceSDK: Failed to retrieve visitor identifiers : " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
### getIdentifiers

This API returns all customer identifiers that were previously synced with the Adobe Experience Cloud.

#### C\#

**Syntax**

```csharp
public static void GetIdentifiers(AdobeGetIdentifiersCallback callback)
```

* _callback_ is a callback containing the previously synced identifiers if the `GetIdentifiers` API executed without any errors.

**Example**

```csharp
[MonoPInvokeCallback(typeof(AdobeGetIdentifiersCallback))]
public static void HandleAdobeGetIdentifiersCallback(string visitorIds)
{
    print("Ids is : " + visitorIds);
}
ACPIdentity.GetIdentifiers(HandleAdobeGetIdentifiersCallback);
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

If an error occurs while retrieving the URL string, _callback_ will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback as an [AdobeCallback](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobecallback) instance:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

When [AdobeCallbackWithError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobecallbackwitherror) is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#adobeerror).

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

{% hint style="info" %}
Method `getUrlVariables` was added in ACPCore version 2.3.0 and ACPIdentity version 2.1.0. Method `getUrlVariablesWithCompletionHandler` was added in ACPCore version 2.5.0 and ACPIdentity version 2.2.0.
{% endhint %}

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

```objectivec
+ (void) getUrlVariables: (nonnull void (^) (NSString* __nullable urlVariables)) callback;
+ (void) getUrlVariablesWithCompletionHandler: (nonnull void (^) (NSString* __nullable urlVariables, NSError* __nullable error)) completionHandler;
```

* _callback_ has an NSString value that contains the visitor identifiers as a querystring after the service request is complete.
* _completionHandler_ is invoked with _urlVariables_ containing the visitor identifiers as a query string, or _error_ if an unexpected error occurs or the request times out. The returned `NSError` contains the [ACPError](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#acperror) code of the specific error. The default timeout is 500ms.

**Examples**

**Objective-C**

```objectivec
[ACPIdentity getUrlVariables:^(NSString * _Nullable urlVariables) {    
  // handle the URL query parameter string here
  NSString* urlString = @"https://example.com";
  NSString* urlStringWithVisitorData = [NSString stringWithFormat:@"%@?%@", urlString, urlVariables];
  NSURL* urlWithVisitorData = [NSURL URLWithString:urlStringWithVisitorData];
  // APIs which update the UI must be called from main thread
  dispatch_async(dispatch_get_main_queue(), ^{
    [[self webView] loadRequest:[NSURLRequest requestWithURL:urlWithVisitorData]];
  }
}];

[ACPIdentity getUrlVariablesWithCompletionHandler:^(NSString * _Nullable urlVariables, NSError * _Nullable error) {
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
ACPIdentity.getUrlVariables {(urlVariables) in
  var urlStringWithVisitorData: String = "https://example.com"
  if let urlVariables: String = urlVariables {
    urlStringWithVisitorData.append("?" + urlVariables)
  }

  guard let urlWithVisitorData: URL = URL(string: urlStringWithVisitorData)   else {
    // handle error, unable to construct URL
    return
  }
  // APIs which update the UI must be called from main thread
  DispatchQueue.main.async {
    self.webView.load(URLRequest(url: urlWithVisitorData))
  }
}

ACPIdentity.getUrlVariables { (urlVariables, error) in
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

{% tab title="React Native" %}
### [getUrlVariables](identity-api-reference.md)

#### JavaScript

{% hint style="info" %}
This method was added in react-native-acpcore v1.0.5.
{% endhint %}

This API gets the Visitor ID Service variables in URL query parameter form, and these variables will be consumed by the hybrid app. This method returns an appropriately formed string that contains the Visitor ID Service URL variables. There will be no leading \(&\) or \(?\) punctuation because the caller is responsible for placing the variables in their resulting java.net.URI in the correct location.

If an error occurs while retrieving the URL string, _callback_ will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

**Syntax**

```jsx
getUrlVariables(): Promise<?string>;
```

**Example**

```jsx
ACPIdentity.getUrlVariables().then(urlVariables => console.log("AdobeExperenceSDK: query params = " + urlVariables));
```
{% endtab %}

{% tab title="Flutter" %}
### getUrlVariables

#### Dart

This API gets the Visitor ID Service variables in URL query parameter form, and these variables will be consumed by the hybrid app. This method returns an appropriately formed string that contains the Visitor ID Service URL variables. There will be no leading \(&\) or \(?\) punctuation because the caller is responsible for placing the variables in their resulting java.net.URI in the correct location.

If an error occurs while retrieving the URL string, _callback_ will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

**Syntax**

```dart
 Future<String> urlVariables;
```

**Example**

```dart
String result = "";

try {
  result = await FlutterACPIdentity.urlVariables;
} on PlatformException {
  log("Failed to get url variables");
}
```
{% endtab %}

{% tab title="Cordova" %}
### [getUrlVariables](identity-api-reference.md)

#### Cordova

This API gets the Visitor ID Service variables in URL query parameter form, and these variables will be consumed by the hybrid app. This method returns an appropriately formed string that contains the Visitor ID Service URL variables. There will be no leading \(&\) or \(?\) punctuation because the caller is responsible for placing the variables in their resulting java.net.URI in the correct location.

If an error occurs while retrieving the URL string, _callback_ will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

**Syntax**

```jsx
ACPIdentity.getUrlVariables(success, fail);
```

* _success_ is a callback containing the url varaibles in query parameter form if the `getUrlVariables` API executed without any errors.
* _fail_ is a callback containing error information if the `getUrlVariables` API was executed with errors.

**Example**

```jsx
ACPIdentity.getUrlVariables(function (handleCallback) {
  console.log("AdobeExperienceSDK: Url variables: " + handleCallback);
}, function (handleError) {
  console.log("AdobeExperenceSDK: Failed to retrieve url variables : " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
### [GetUrlVariables](identity-api-reference.md)

#### C\#

This API gets the Visitor ID Service variables in URL query parameter form, and these variables will be consumed by the hybrid app. This method returns an appropriately formed string that contains the Visitor ID Service URL variables. There will be no leading \(&\) or \(?\) punctuation because the caller is responsible for placing the variables in their resulting java.net.URI in the correct location.

If an error occurs while retrieving the URL string, _callback_ will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID \(ECID\)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID \(AID\), if available from the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID \(VID\), if previously set in the [Analytics extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).

**Syntax**

```csharp
public static void GetUrlVariables(AdobeGetUrlVariables callback)
```

* _callback_ is a callback containing the url varaibles in query parameter form if the `GetUrlVariables` API executed without any errors.

**Example**

```csharp
[MonoPInvokeCallback(typeof(AdobeGetUrlVariables))]
public static void HandleAdobeGetUrlVariables(string urlVariables)
{
  print("Url variables are : " + urlVariables);
}
ACPIdentity.GetUrlVariables(HandleAdobeGetUrlVariables);
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

Register the Identity extension in your app's `didFinishLaunchingWithOptions` function:

**Objective-C**

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```

**Swift**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  ACPIdentity.registerExtension();
  // Override point for customization after application launch.
  return true;
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

When using React Native, registering Identity with Mobile Core should be done in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Flutter" %}
#### Dart

When using Flutter, registering Identity with Mobile Core should be done in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Cordova" %}
## Cordova

When using Cordova, registering Identity with Mobile Core should be done in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Unity" %}
## C\#

Register the Identity extension in your app's `Start()` function:

```csharp
void Start() {
  ACPIdentity.RegisterExtension();
}
```
{% endtab %}
{% endtabs %}

## setAdvertisingIdentifier

The advertising ID is preserved between app upgrades, is saved and restored during the standard application backup process, available via [Signals](identity-api-reference.md), and is removed at uninstall.

{% hint style="info" %}
If the current SDK privacy status is `optedout`, the advertising identifier is not set or stored.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### setAdvertisingIdentifier

This API sets the provided advertising identifier.

#### Java

**Syntax**

```java
public static void setAdvertisingIdentifier(final String advertisingIdentifier);
```

* _advertisingIdentifier_ is a string that provides developers with a simple, standard system to track the Ads through their apps.     

**Example**

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
### setAdvertisingIdentifier

{% hint style="info" %}
Retrieve the Identifier for Advertising \(IDFA\) from Apple APIs only if you are using an ad service. If you retrieve IDFA, and are not using it properly, your app might be rejected.
{% endhint %}

{% hint style="warning" %}
This is just an implementation example. For more information about IDFA and how to handle them correctly in your mobile application, see [Apple developer documentation about IDFA](https://developer.apple.com/documentation/adsupport/asidentifiermanager)
{% endhint %}

#### iOS

**Syntax**

```objectivec
+ (void) setAdvertisingIdentifier: (nullable NSString*) adId;
```

* _adId_ is a string that provides developers with a simple, standard system to continue to track the Ads through their apps.    

**Example**

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
### setAdvertisingIdentifier

#### JavaScript

**Syntax**

```jsx
setAdvertisingIdentifier(advertisingIdentifier?: String);
```

* _adID_ is a string that provides developers with a simple, standard system to continue to track the Ads through their apps.

**Example**

```jsx
ACPCore.setAdvertisingIdentifier("ADVTID");
```
{% endtab %}

{% tab title="Flutter" %}
### setAdvertisingIdentifier

#### Dart

**Syntax**

```dart
Future<void> setAdvertisingIdentifier (String aid);
```

* _aid_ is a string that provides developers with a simple, standard system to continue to track the Ads through their apps.

**Example**

```dart
FlutterACPCore.setAdvertisingIdentifier("ADVTID");
```
{% endtab %}

{% tab title="Cordova" %}
### setAdvertisingIdentifier

#### Cordova

**Syntax**

```jsx
ACPCore.setAdvertisingIdentifier(identifier, success, fail);
```

* _identifier_ _\(String\)_ provides developers with a simple, standard system to continue to track the Ads through their apps.
* _success_ is a callback containing a general success message if the `setAdvertisingIdentifier` API executed without any errors.
* _fail_ is a callback containing error information if the `setAdvertisingIdentifier` API was executed with errors.

**Example**

```jsx
ACPCore.setAdvertisingIdentifier("ADVTID", function (handleCallback) {
  console.log("AdobeExperienceSDK: Advertising identifier successfully set.");
}, function (handleError) {
  console.log("AdobeExperenceSDK: Failed to set advertising identifier : " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
### SetAdvertisingIdentifier

#### C\#

**Syntax**

```csharp
public static void SetAdvertisingIdentifier(string adId)
```

* _adId_ _\(String\)_ provides developers with a simple, standard system to continue to track the Ads through their apps.

**Example**

```csharp
ACPCore.SetAdvertisingIdentifier("ADVTID");
```
{% endtab %}
{% endtabs %}

## setPushIdentifier

This API sets the device token for push notifications in the SDK. If the current SDK privacy status is `optedout`, the push identifier is not set.

{% tabs %}
{% tab title="Android" %}
### setPushIdentifier

#### Java

**Syntax**

```java
public static void setPushIdentifier(final String pushIdentifier);
```

* _pushIdentifier_  is a string that contains the device token for push notifications.

**Example**

```java
//Retrieve the token from either GCM or FCM, and pass it to the SDK
MobileCore.setPushIdentifier(token);
```
{% endtab %}

{% tab title="iOS" %}
### setPushIdentifier

#### iOS

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

* _deviceToken_  is a string that contains the device token for push notifications.

**Example**

**Objective-C**

```objectivec
// Set the deviceToken that the APNS has assigned to the device
[ACPCore setPushIdentifier:deviceToken];
```

**Swift**

```swift
// Set the deviceToken that the APNs has assigned to the device
ACPCore.setPushIdentifier(deviceToken)
```
{% endtab %}

{% tab title="React Native" %}
### setPushIdentifier

#### JavaScript

**Syntax**

```jsx
ACPCore.setPushIdentifier(pushIdentifier);
```

* _pushIdentifier_ is a string that contains the device token for push notifications.

**Example**

```jsx
ACPCore.setPushIdentifier("pushID");
```
{% endtab %}
{% endtabs %}

## syncIdentifier

The `syncIdentifier()` and `syncIdentifiers()` APIs update the specified customer IDs with the Adobe Experience Cloud ID \(ECID\) Service.

These APIs synchronize the provided customer identifier type key and value with the authentication state to the ECID Service. If the specified customer ID type exists in the service, this ID type is updated with the new ID and the authentication state. Otherwise, a new customer ID is added.

Starting with _ACPIdentity v2.1.3 \(iOS\)_ and _Identity v1.1.2 \(Android\)_ if the new `identifier` value is null or empty, this ID type is removed from the local storage, Identity shared state and not synced with the Adobe ECID Service.

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

```objectivec
+ (void) syncIdentifier: (nonnull NSString*) identifierType             
             identifier: (nonnull NSString*) identifier
         authentication: (ADBMobileVisitorAuthenticationState) authenticationState;
```

* The _identifierType \(String\)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier \(String\)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifier type` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* The _authenticationState \(VisitorIDAuthenticationState\)_ value indicates the authentication state for the user and contains one of the following `VisitorID.AuthenticationState` values:
  * `ACPMobileVisitorAuthenticationStateAuthenticated`
  * `ACPMobileVisitorAuthenticationStateLoggedOut`
  * `ACPMobileVisitorAuthenticationStateUnknown`

**Examples**

**Objective-C**

```objectivec
[ACPIdentity syncIdentifier:@"idType" identifier:@"idValue" authentication:ACPMobileVisitorAuthenticationStateUnknown];
```

**Swift**

```swift
ACPIdentity.syncIdentifier("idType", identifier: "idValue", authentication: ACPMobileVisitorAuthenticationState.unknown)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```jsx
syncIdentifier(identifierType: String, identifier: String, authenticationState: string);
```

* The _identifierType \(String\)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier \(String\)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifier type` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* _authenticationState \(VisitorIDAuthenticationState\)_ value indicating authentication state for the user and contains one of the following `VisitorID.AuthenticationState` values:
* `ACPMobileVisitorAuthenticationState.AUTHENTICATED`
* `ACPMobileVisitorAuthenticationState.LOGGED_OUT`
* `ACPMobileVisitorAuthenticationState.UNKNOWN`

**Example**

```jsx
import {ACPMobileVisitorAuthenticationState} from '@adobe/react-native-acpcore';

ACPIdentity.syncIdentifier("identifierType", "identifier", ACPMobileVisitorAuthenticationState.AUTHENTICATED);
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

**Syntax**

```dart
Future<void> syncIdentifier(String identifierType, String identifier, ACPMobileVisitorAuthenticationState authState);
```

* The _identifierType \(String\)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier \(String\)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifier type` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* _authState_ value indicating authentication state for the user and contains one of the following `ACPMobileVisitorAuthenticationState` values:
* `ACPMobileVisitorAuthenticationState.AUTHENTICATED`
* `ACPMobileVisitorAuthenticationState.LOGGED_OUT`
* `ACPMobileVisitorAuthenticationState.UNKNOWN`

**Example**

```dart
import 'package:flutter_acpcore/src/acpmobile_visitor_id.dart';

FlutterACPIdentity.syncIdentifier("identifierType", "identifier", ACPMobileVisitorAuthenticationState.AUTHENTICATED);
```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

**Syntax**

```jsx
ACPIdentity.syncIdentifier = function(identifierType, identifier, authState, success, fail);
```

* The _identifierType \(String\)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier \(String\)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifier type` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* _authState_ value indicating authentication state for the user and contains one of the following `ACPMobileVisitorAuthenticationState` values:
  * `ACPIdentity.ACPMobileVisitorAuthenticationStateAuthenticated`
  * `ACPIdentity.ACPMobileVisitorAuthenticationStateLoggedOut`
  * `ACPIdentity.ACPMobileVisitorAuthenticationStateUnknown`
* _success_ is a callback containing the visitor id type, value, and authentication state if the `syncIdentifier` API executed without any errors.
* _fail_ is a callback containing error information if the `syncIdentifier` API was executed with errors.

**Example**

```jsx
ACPIdentity.syncIdentifier("id1", "value1", ACPIdentity.ACPMobileVisitorAuthenticationStateUnknown, function (handleCallback) {
  console.log("AdobeExperenceSDK: Identifier synced successfully : " + handleCallback);
}, function (handleError) {
  console.log("AdobeExperenceSDK: Failed to sync identifier : " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
#### C\#

**Syntax**

```csharp
public static void SyncIdentifier(string identifierType, string identifier, ACPAuthenticationState authState)
```

* The _identifierType \(String\)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier \(String\)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifier type` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* _authState_ value indicating authentication state for the user and contains one of the following `ACPAuthenticationState` values:
  * `ACPIdentity.ACPAuthenticationState.AUTHENTICATED`
  * `ACPIdentity.ACPAuthenticationState.UNKNOWN`
  * `ACPIdentity.ACPAuthenticationState.LOGGED_OUT`

**Example**

```text
ACPIdentity.SyncIdentifier("idType1", "idValue1", ACPIdentity.ACPAuthenticationState.AUTHENTICATED);
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

```objectivec
+ (void) syncIdentifiers: (nullable NSDictionary*) identifiers;
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

**Examples**

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

**Syntax**

```jsx
syncIdentifiers(identifiers?: {string: string});
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

**Example**

```jsx
ACPIdentity.syncIdentifiers({"id1": "identifier1"});
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

**Syntax**

```dart
Future<void> syncIdentifiers (Map<String, String> identifiers);
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

**Example**

```jsx
FlutterACPIdentity.syncIdentifiers({"idType1":"idValue1",
                                    "idType2":"idValue2",
                                    "idType3":"idValue3"});
```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

**Syntax**

```jsx
ACPIdentity.syncIdentifiers = function(identifiers, success, fail);
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

* _success_ is a callback containing the synced identifiers if the `syncIdentifiers` API executed without any errors.
* _fail_ is a callback containing error information if the `syncIdentifiers` API was executed with errors.

**Example**

```jsx
ACPIdentity.syncIdentifiers({"idType1":"idValue1", "idType2":"idValue2", "idType3":"idValue3"}, function (handleCallback) {
  console.log("AdobeExperienceSDK: " + handleCallback)
}, function (handleError) {
  console.log("AdobeExperenceSDK: Failed to sync identifiers : " + handleError)
});
```
{% endtab %}

{% tab title="Unity" %}
#### C\#

**Syntax**

```csharp
ublic static void SyncIdentifiers(Dictionary<string, string> identifiers)
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

**Example**

```csharp
Dictionary<string, string> ids = new Dictionary<string, string>();
ids.Add("idsType1", "idValue1");
ids.Add("idsType2", "idValue2");
ids.Add("idsType3", "idValue3");
ACPIdentity.SyncIdentifiers(ids);
```
{% endtab %}
{% endtabs %}

## syncIdentifiers \(overloaded\)

The function of this API is the same as the `syncIdentifier` API. This API passes a list of identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value. In each identifier pair, if the `identifier type` contains a null or an empty string, the identifier is ignored by the Identity extension.

Starting with _ACPIdentity v2.1.3 \(iOS\)_ and _Identity v1.1.2 \(Android\)_ if the new `identifier` value is null or empty, this ID type is removed from the local storage, Identity shared state and not synced with the Adobe ECID Service.

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

```objectivec
+ (void) syncIdentifiers: (nullable NSDictionary*) identifiers authentication: (ACPMobileVisitorAuthenticationState) authenticationState;
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

* The _authenticationState \(VisitorIDAuthenticationState\)_ indicates the authentication state of the user and contains one of the `VisitorID.AuthenticationState` values:
  * `ACPMobileVisitorAuthenticationState.AUTHENTICATED`
  * `ACPMobileVisitorAuthenticationState.LOGGED_OUT`
  * `ACPMobileVisitorAuthenticationState.UNKNOWN`

**Examples**

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
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```jsx
syncIdentifiersWithAuthState(identifiers?: {string: string}, authenticationState: string);
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

* The _authenticationState \(ACPMobileVisitorAuthenticationState\)_ indicates the authentication state of the user and contains one of the `ACPMobileVisitorAuthenticationState` values:
  * `ACPMobileVisitorAuthenticationState.AUTHENTICATED`
  * `ACPMobileVisitorAuthenticationState.LOGGED_OUT`
  * `ACPMobileVisitorAuthenticationState.UNKNOWN`

**Example**

```jsx
import {ACPMobileVisitorAuthenticationState} from '@adobe/react-native-acpcore';

ACPIdentity.syncIdentifiersWithAuthState({"id1": "identifier1"}, ACPMobileVisitorAuthenticationState.UNKNOWN);
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

**Syntax**

```dart
Future<void> syncIdentifiersWithAuthState (Map<String, String> identifiers, ACPMobileVisitorAuthenticationState authState);
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

* The _authState_ \(ACPMobileVisitorAuthenticationState\)\_ indicates the authentication state of the user and contains one of the `ACPMobileVisitorAuthenticationState` values:
  * `ACPMobileVisitorAuthenticationState.AUTHENTICATED`
  * `ACPMobileVisitorAuthenticationState.LOGGED_OUT`
  * `ACPMobileVisitorAuthenticationState.UNKNOWN`

**Example**

```dart
import 'package:flutter_acpcore/src/acpmobile_visitor_id.dart';

FlutterACPIdentity.syncIdentifiersWithAuthState({"idType1":"idValue1", "idType2":"idValue2", "idType3":"idValue3"}, ACPMobileVisitorAuthenticationState.UNKNOWN);
```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

**Syntax**

```jsx
ACPIdentity.syncIdentifiers = function(identifiers, authState, success, fail);
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

* _authState_ value indicating authentication state for the identifiers to be synced and contains one of the `ACPMobileVisitorAuthenticationState` values:
  * `ACPIdentity.ACPMobileVisitorAuthenticationStateAuthenticated`
  * `ACPIdentity.ACPMobileVisitorAuthenticationStateLoggedOut`
  * `ACPIdentity.ACPMobileVisitorAuthenticationStateUnknown`
* _success_ is a callback containing the synced identifiers if the `syncIdentifiers` API executed without any errors.
* _fail_ is a callback containing error information if the `syncIdentifiers` API was executed with errors.

**Example**

```jsx
ACPIdentity.syncIdentifiers({"idType1":"idValue1", "idType2":"idValue2", "idType3":"idValue3"}, ACPIdentity.ACPMobileVisitorAuthenticationStateAuthenticated, function (handleCallback) {
  console.log("AdobeExperienceSDK: " + handleCallback)
}, function (handleError) {
  console.log("AdobeExperenceSDK: Failed to sync identifiers : " + handleError)
});
```
{% endtab %}

{% tab title="Unity" %}
#### C\#

**Syntax**

```csharp
public static void SyncIdentifiers(Dictionary<string, string> ids, ACPAuthenticationState authenticationState)
```

* The _ids_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

* _authenticationState_ value indicating authentication state for the identifiers to be synced and contains one of the `VisitorID.AuthenticationState` values:
  * `VisitorID.AuthenticationState.AUTHENTICATED`
  * `VisitorID.AuthenticationState.LOGGED_OUT`
  * `VisitorID.AuthenticationState.UNKNOWN`

**Example**

```csharp
Dictionary<string, string> ids = new Dictionary<string, string>();
ids.Add("idsType1", "idValue1");
ids.Add("idsType2", "idValue2");
ids.Add("idsType3", "idValue3");
ACPIdentity.SyncIdentifiers(ids, ACPIdentity.ACPAuthenticationState.AUTHENTICATED);
ACPIdentity.SyncIdentifiers(ids, ACPIdentity.ACPAuthenticationState.LOGGED_OUT);
ACPIdentity.SyncIdentifiers(ids, ACPIdentity.ACPAuthenticationState.UNKNOWN);
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

**ACPMobileVisitorAuthenticationState**

This is used to indicate the authentication state for the current `VisitorID`.

```objectivec
typedef NS_ENUM(NSUInteger,
    ADBMobileVisitorAuthenticationState) {    
    ACPMobileVisitorAuthenticationStateUnknown          = 0,    
    ACPMobileVisitorAuthenticationStateAuthenticated    = 1,    
    ACPMobileVisitorAuthenticationStateLoggedOut        = 2  };
```

**ACPMobileVisitorId**

This is an identifier to be used with the Experience Cloud Visitor ID Service and it contains the origin, the identifier type, the identifier,, and the authentication state of the visitor ID.

```objectivec
@interface ACPMobileVisitorId : NSObject

@property(nonatomic, strong, nullable) NSString* idOrigin;
@property(nonatomic, strong, nullable) NSString* idType;
@property(nonatomic, strong, nullable) NSString* identifier;
@property(nonatomic, readwrite) ACPMobileVisitorAuthenticationState authenticationState;

@end
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**ACPVisitorID**

This is an identifier to be used with the Experience Cloud Visitor ID Service and it contains the origin, the identifier type, the identifier, and the authentication state of the visitor ID.

```jsx
import {ACPVisitorID} from '@adobe/react-native-acpcore';

var visitorId = new ACPVisitorID(idOrigin?: string, idType: string, id?: string, authenticationState?: ACPMobileVisitorAuthenticationState);
```

**ACPMobileVisitorAuthenticationState**

This is used to indicate the authentication state for the current `VisitorID`.

```jsx
import {ACPMobileVisitorAuthenticationState} from '@adobe/react-native-acpcore';

var state = ACPMobileVisitorAuthenticationState.AUTHENTICATED;
//var state = ACPMobileVisitorAuthenticationState.LOGGED_OUT;
//var state = ACPMobileVisitorAuthenticationState.UNKNOWN;
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

**ACPVisitorID**

This is an identifier to be used with the Experience Cloud Visitor ID Service and it contains the origin, the identifier type, the identifier, and the authentication state of the visitor ID.

```dart
import 'package:flutter_acpcore/src/acpmobile_visitor_id.dart';


class ACPMobileVisitorId {
  String get idOrigin;
  String get idType;
  String get identifier;
  ACPMobileVisitorAuthenticationState get authenticationState;
};
```

**ACPMobileVisitorAuthenticationState**

This is used to indicate the authentication state for the current `VisitorID`.

```dart
import 'package:flutter_acpcore/src/acpmobile_visitor_id.dart';

enum ACPMobileVisitorAuthenticationState {UNKNOWN, AUTHENTICATED, LOGGED_OUT};
```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

**ACPMobileVisitorAuthenticationState**

This is used to indicate the authentication state for the current `VisitorID`.

```jsx
ACPIdentity.ACPMobileVisitorAuthenticationStateUnknown = 0;
ACPIdentity.ACPMobileVisitorAuthenticationStateAuthenticated = 1;
ACPIdentity.ACPMobileVisitorAuthenticationStateLoggedOut = 2;
```
{% endtab %}

{% tab title="Unity" %}
#### C\#

**ACPAuthenticationState**

This is used to indicate the authentication state for the current `VisitorID`.

```csharp
ACPIdentity.ACPAuthenticationState.UNKNOWN = 0;
ACPIdentity.ACPAuthenticationState.AUTHENTICATED = 1;
ACPIdentity.ACPAuthenticationState.LOGGED_OUT = 2;
```
{% endtab %}
{% endtabs %}

