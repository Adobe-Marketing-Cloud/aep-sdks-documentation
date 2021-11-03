# Identity API reference

## appendToURL
## appendVisitorInfoForURL

This API appends Adobe visitor information to the query component of the specified URL.

If the provided URL is null or empty, it is returned as is. Otherwise, the following information is added to the query component of the specified URL and is returned in the callback function:

* The `adobe_mc` attribute is a URL encoded list that contains:
  * `MCMID` - Experience Cloud ID (ECID)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID (AID), if available from the [Analytics extension](../../using-mobile-extensions/adobe-analytics/analytics-api-reference#gettrackingidentifier)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID (VID), if previously set in the [Analytics extension](../../using-mobile-extensions/adobe-analytics/analytics-api-reference#setidentifier).

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

If your application uses more complicated URLs, such as Angular URLs, you should use [getUrlVariables](identity-api-reference.md#geturlvariables).
{% endhint %}

{% tabs %}
{% tab title="Android" %}


#### Java

### appendVisitorInfoForURL

When [AdobeCallbackWithError](../mobile-core-api-reference#adobecallbackwitherror) is provided in replace of [AdobeCallback](../mobile-core-api-reference#adobecallback), and you are fetching the attributes from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core-api-reference#adobeerror).

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

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### appendToURL

#### iOS

**Syntax**

```swift
static func appendTo(url: URL?, completion: @escaping (URL?, Error?) -> Void)
```

* _url_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
* _completion_ is invoked after the updated _URL_ is available or _Error_ if an unexpected exception occurs or the request times out. The returned `Error` contains the [AEPError](../mobile-core-api-reference#aeperror) code of the specific error. The default timeout is 1000ms.

**Examples**

**Swift**

```swift
Identity.appendTo(url: URL(string: "https://example.com")) { appendedURL, error in
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

**Objective-C**

```objectivec
NSURL* url = [NSURL URLWithString:@"https://example.com"];
[AEPMobileIdentity appendToUrl:url completion:^(NSURL * _Nullable urlWithVisitorData, NSError * _Nullable error) {
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

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### appendToURL

{% hint style="info" %}
Method `appendToUrl:withCompletionHandler` was added in ACPCore version 2.5.0 and ACPIdentity version 2.2.0.
{% endhint %}

#### iOS

**Syntax**

```objectivec
+ (void) appendToUrl: (nullable NSURL*) baseUrl withCallback: (nullable void (^) (NSURL* __nullable urlWithVisitorData)) callback;
+ (void) appendToUrl: (nullable NSURL*) baseUrl withCompletionHandler: (nullable void (^) (NSURL* __nullable urlWithVersionData, NSError* __nullable error)) completionHandler;
```

* _baseUrl_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
* _callback_ is invoked after the updated URL is available.
* _completionHandler_ is invoked with _urlWithVersionData_ after the updated URL is available or _error_ if an unexpected exception occurs or the request times out. The returned `NSError` contains the [ACPError](../../using-mobile-extensions/mobile-core/mobile-core-api-reference#acperror) code of the specific error. The default timeout is 500ms.

**Examples**

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

{% endtab %}

{% tab title="React Native" %}
### appendVisitorInfoForURL

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
{% endtab %}

{% tab title="Flutter" %}
### appendVisitorInfoForURL

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

{% endtab %}

{% tab title="Cordova" %}
### appendVisitorInfoForURL

#### Cordova

**Syntax**

```jsx
ACPIdentity.appendVisitorInfoForUrl = function(url, success, fail);
```

* _url_ _(String)_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
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

{% endtab %}

{% tab title="Unity" %}
### AppendToUrl

#### C\#

**Syntax**

```csharp
public static void AppendToUrl(string url, AdobeIdentityAppendToUrlCallback callback)
```

* _url_ _(String)_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
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

{% endtab %}

{% tab title="Xamarin" %}
### AppendToUrl

#### C\#

**iOS Syntax**

```csharp
public unsafe static void AppendToUrl (NSUrl baseUrl, Action<NSUrl> callback);
```

* baseUrl _(NSUrl)_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
* _callback_ is a callback containing the provided URL with the visitor information appended if the `AppendToUrl` API executed without any errors.

**Android Syntax**

```csharp
public unsafe static void AppendVisitorInfoForURL (string baseURL, IAdobeCallback callback);
```

* baseURL _(string)_ is the URL to which the visitor information needs to be appended. If the visitor information is nil or empty, the URL is returned as is.
* _callback_ is a callback containing the provided URL with the visitor information appended if the `AppendVisitorInfoForURL` API executed without any errors.

**iOS Example**

```csharp
ACPIdentity.AppendToUrl(url, callback => {
  Console.WriteLine("Appended url: " + callback);
});
```

**Android Example**

```csharp
ACPIdentity.AppendVisitorInfoForURL("https://example.com", new StringCallback());

class StringCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("Appended url: " + stringContent);
    } 
    else 
    {
      Console.WriteLine("null content in string callback");
    }
  }
}
```

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

{% tab title="iOS (AEP 3.x)" %}
#### iOS

**Swift**

```swift
let identityExtensionVersion  = Identity.extensionVersion
```

**Objective-C**

```objectivec
NSString *identityVersion = [AEPMobileIdentity extensionVersion];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### iOS

**Swift**

```swift
let identityVersion  = ACPIdentity.extensionVersion()
```

**Objective-C**

```objectivec
NSString *identityVersion = [ACPIdentity extensionVersion];
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

{% tab title="Xamarin" %}
#### C\#

**Syntax**

```csharp
public static string ExtensionVersion ();
```

**Example**

```csharp
string identityVersion = ACPIdentity.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

## getExperienceCloudId

This API retrieves the ECID that was generated when the app was initially launched and is stored in the ECID Service.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall.

{% tabs %}
{% tab title="Android" %}
### getExperienceCloudId

When [AdobeCallbackWithError](../mobile-core-api-reference#adobecallbackwitherror) is provided in replace of [AdobeCallback](../mobile-core-api-reference#adobecallback), and you are fetching the ECID from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core-api-reference#adobeerror).

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

{% tab title="iOS (AEP 3.x)" %}
### getExperienceCloudId

**Syntax**

```swift
@objc(getExperienceCloudId:)
static func getExperienceCloudId(completion: @escaping (String?, Error?) -> Void)
```

* _completion_ is invoked with _String_ after the ECID is available, or _Error_ if an unexpected error occurs or the request times out. The returned `Error` contains the [AEPError](../mobile-core-api-reference#aeperror) code of the specific error. The default timeout is 1000ms.

**Examples**

**Swift**

```swift
Identity.getExperienceCloudId { ecid, error in
  if let error = error {
    // handle error here
  } else {
    // handle the retrieved ID here
  }
}
```

**Objective-C**

```objectivec
[AEPMobileIdentity getExperienceCloudId:^(NSString * _Nullable ecid, NSError *error) {
  if (error) {
    // handle error here
  } else {
    // handle the retrieved ID here
  }
}];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### getExperienceCloudId

{% hint style="info" %}
Method `getExperienceCloudIdWithCompletionHandler` was added in ACPCore version 2.5.0 and ACPIdentity version 2.2.0.
{% endhint %}

**Syntax**

```objective-c
+ (void) getExperienceCloudId: (nonnull void (^) (NSString* __nullable experienceCloudId)) callback;
+ (void) getExperienceCloudIdWithCompletionHandler: (nonnull void (^) (NSString* __nullable experienceCloudId, NSError* __nullable error)) completionHandler;
```

* _callback_ is invoked after the ECID is available.
* _completionHandler_ is invoked with _experienceCloudId_ after the ECID is available, or _error_ if an unexpected error occurs or the request times out. The returned `NSError` contains the [ACPError](../mobile-core-api-reference#acperror) code of the specific error. The default timeout is 500ms.

**Examples**

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

{% endtab %}

{% tab title="React Native" %}
### getExperienceCloudId

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

#### C\#

#### Syntax

```csharp
public static void GetExperienceCloudId(AdobeGetExperienceCloudIdCallback callback)
```

* _callback_ is a callback containing the experience cloud id if the `GetExperienceCloudId` API executed without any errors.

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

{% tab title="Xamarin" %}
### getExperienceCloudId

#### C\#

#### iOS Syntax

```csharp
public unsafe static void GetExperienceCloudId (Action<NSString> callback);
```

* _callback_ is a callback containing the experience cloud id if the `getExperienceCloudId` API executed without any errors.

#### Android Syntax

```csharp
public unsafe static void GetExperienceCloudId (IAdobeCallback callback);
```

* _callback_ is a callback containing the experience cloud id if the `getExperienceCloudId` API executed without any errors.

#### iOS Example

```csharp
ACPIdentity.GetExperienceCloudId(callback => {
  Console.WriteLine("Experience cloud id: " + callback);
});
```

#### Android Example

```csharp
ACPIdentity.GetExperienceCloudId(new StringCallback());

class StringCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("Experience cloud id: " + stringContent);
    } 
    else 
    {
      Console.WriteLine("null content in string callback");
    }
  }
}
```
{% endtab %}
{% endtabs %}

## getIdentifiers

This API returns all customer identifiers that were previously synced with the Adobe Experience Cloud.

{% tabs %}
{% tab title="Android" %}

### getIdentifiers

When [AdobeCallbackWithError](../mobile-core-api-reference#adobecallbackwitherror) is provided in replace of [AdobeCallback](../mobile-core-api-reference#adobecallback), and you are fetching the custom identifiers from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core-api-reference#adobeerror).

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

{% tab title="iOS (AEP 3.x)" %}

### getIdentifiers

#### iOS

**Syntax**

```swift
@objc(getIdentifiers:)
static func getIdentifiers(completion: @escaping ([Identifiable]?, Error?) -> Void)
```

* _completion_ is invoked with a list of  _Identifiable_ objects after the customer identifiers are available, or _Error_ if an unexpected error occurs or the request times out. The returned `Error` contains the [AEPError](../mobile-core-api-reference#aeperror) code of the specific error. The default timeout is 1000ms.

**Examples**

**Swift**

```swift
Identity.getIdentifiers { identifiers, error in
  if let error = error {
    // handle error here
  } else {
    // handle the retrieved identifiers here
  }
}
```

**Objective-C**

```objectivec
[[AEPMobileIdentity getIdentifiers:^(NSArray<id<AEPIdentifiable>> * _Nullable identifiers, NSError *error) {
  if (error) {
    // handle error here
  } else {
    // handle the retrieved identifiers here
  }
}];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### getIdentifiers

{% hint style="info" %}
Method `getIdentifiersWithCompletionHandler` was added in ACPCore version 2.5.0 and ACPIdentity version 2.2.0.
{% endhint %}

#### iOS

**Syntax**

```objectivec
+ (void) getIdentifiers: (nonnull void (^) (NSArray<ADBMobileVisitorId*>* __nullable visitorIDs)) callback;
+ (void) getIdentifiersWithCompletionHandler: (nonnull void (^) (NSArray<ACPMobileVisitorId*>* __nullable visitorIDs, NSError* __nullable error)) completionHandler;
```

* _callback_ is invoked after the customer identifiers are available.
* _completionHandler_ is invoked with _visitorIDs_ after the customer identifiers are available, or _error_ if an unexpected error occurs or the request times out. The returned `NSError` contains the [ACPError](../mobile-core-api-reference#acperror) code of the specific error. The default timeout is 500ms.

**Examples**
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
{% endtab %}

{% tab title="React Native" %}
### getIdentifiers

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

{% tab title="Xamarin" %}
### getIdentifiers

#### C\#

**iOS Syntax**

```csharp
public unsafe static void GetIdentifiers (Action<ACPMobileVisitorId[]> callback);
```

* _callback_ is a callback containing the previously synced identifiers if the `GetIdentifiers` API executed without any errors.

**Android Syntax**

```csharp
public unsafe static void GetIdentifiers (IAdobeCallback callback);
```

* _callback_ is a callback containing the previously synced identifiers if the `GetIdentifiers` API executed without any errors.

**iOS Example**

```csharp
Action<ACPMobileVisitorId[]> callback = new Action<ACPMobileVisitorId[]>(handleCallback);
ACPIdentity.GetIdentifiers(callback);

private void handleCallback(ACPMobileVisitorId[] ids)
{
  String visitorIdsString = "[]";
  if (ids.Length != 0)
  {
    visitorIdsString = "";
    foreach (ACPMobileVisitorId id in ids)
    {
      visitorIdsString = visitorIdsString + "[Id: " + id.Identifier + ", Type: " + id.IdType + ", Origin: " + id.IdOrigin + ", Authentication: " + id.AuthenticationState + "]";
    }
  }
  Console.WriteLine("Retrieved visitor ids: " + visitorIdsString);
}
```

**Android Example**

```csharp
ACPIdentity.GetIdentifiers(new GetIdentifiersCallback());

class GetIdentifiersCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object retrievedIds)
  {
    System.String visitorIdsString = "[]";
    if (retrievedIds != null)
    {
      var ids = GetObject<JavaList>(retrievedIds.Handle, JniHandleOwnership.DoNotTransfer);
      if (ids != null && ids.Count > 0)
      {
        visitorIdsString = "";
        foreach (VisitorID id in ids)
        {
          visitorIdsString = visitorIdsString + "[Id: " + id.Id + ", Type: " + id.IdType + ", Origin: " + id.IdOrigin + ", Authentication: " + id.GetAuthenticationState() + "]";
        }
      }
    }
    Console.WriteLine("Retrieved visitor ids: " + visitorIdsString);
  }
}
```
{% endtab %}
{% endtabs %}

## getUrlVariables

This API gets the Visitor ID Service variables in URL query parameter form, and these variables will be consumed by the hybrid app. This method returns an appropriately formed string that contains the Visitor ID Service URL variables. There will be no leading (&) or (?) punctuation because the caller is responsible for placing the variables in their resulting URL in the correct location.

If an error occurs while retrieving the URL string, the callback handler will be called with a null value. Otherwise, the following information is added to the string that is returned in the callback:

* The `adobe_mc` attribute is an URL encoded list that contains:
  * `MCMID` - Experience Cloud ID (ECID)
  * `MCORGID` - Experience Cloud Org ID
  * `MCAID` - Analytics Tracking ID (AID), if available from the [Analytics extension](../../../using-mobile-extensions/adobe-analytics)
  * `TS` - A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID (VID), if previously set in the [Analytics extension](../../../using-mobile-extensions/adobe-analytics).

{% tabs %}
{% tab title="Android" %}

### getUrlVariables

{% hint style="info" %}
This method was added in Core version 1.4.0 and Identity version 1.1.0_._
{% endhint %}

When [AdobeCallbackWithError](../mobile-core-api-reference#adobecallbackwitherror) is provided in replace of [AdobeCallback](../mobile-core-api-reference#adobecallback), and you are fetching the attributes from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core-api-reference#adobeerror).

#### Java

**Syntax**

```java
public static void getUrlVariables(final AdobeCallback<String> callback);
```

* _callback_ has an NSString value that contains the visitor identifiers as a query string after the service request is complete.

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

{% tab title="iOS (AEP 3.x)" %}
### getUrlVariables

#### iOS

**Syntax**

```swift
@objc(getUrlVariables:)
static func getUrlVariables(completion: @escaping (String?, Error?) -> Void)
```

* _completion_ is invoked with _String_ containing the visitor identifiers as a query string, or _Error_ if an unexpected error occurs or the request times out. The returned `Error` contains the [AEPError](../mobile-core-api-reference#aeperror) code of the specific error. The default timeout is 500ms.

**Examples**

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

**Objective-C**

```objectivec
[AEPMobileIdentity getUrlVariables:^(NSString * _Nullable urlVariables, NSError *error) {
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

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### getUrlVariables

{% hint style="info" %}
Method `getUrlVariables` was added in ACPCore version 2.3.0 and ACPIdentity version 2.1.0. Method `getUrlVariablesWithCompletionHandler` was added in ACPCore version 2.5.0 and ACPIdentity version 2.2.0.
{% endhint %}

#### iOS

**Syntax**

```objectivec
+ (void) getUrlVariables: (nonnull void (^) (NSString* __nullable urlVariables)) callback;
+ (void) getUrlVariablesWithCompletionHandler: (nonnull void (^) (NSString* __nullable urlVariables, NSError* __nullable error)) completionHandler;
```

* _callback_ has an NSString value that contains the visitor identifiers as a query string after the service request is complete.
* _completionHandler_ is invoked with _urlVariables_ containing the visitor identifiers as a query string, or _error_ if an unexpected error occurs or the request times out. The returned `NSError` contains the [ACPError](../mobile-core-api-reference#acperror) code of the specific error. The default timeout is 500ms.

**Examples**

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

{% endtab %}

{% tab title="React Native" %}
### [getUrlVariables](identity-api-reference.md)

#### JavaScript

{% hint style="info" %}
This method was added in react-native-acpcore v1.0.5.
{% endhint %}

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

**Syntax**

```jsx
ACPIdentity.getUrlVariables(success, fail);
```

* _success_ is a callback containing the url variables in query parameter form if the `getUrlVariables` API executed without any errors.
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

**Syntax**

```csharp
public static void GetUrlVariables(AdobeGetUrlVariables callback)
```

* _callback_ is a callback containing the url variables in query parameter form if the `GetUrlVariables` API executed without any errors.

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

{% tab title="Xamarin" %}
### [GetUrlVariables](identity-api-reference.md)

#### C\#

**iOS Syntax**

```csharp
public unsafe static void GetUrlVariables (Action<NSString> callback);
```

* _callback_ is a callback containing the url variables in query parameter form if the `GetUrlVariables` API executed without any errors.

**Android Syntax**

```csharp
public unsafe static void GetUrlVariables (IAdobeCallback callback);
```

* _callback_ is a callback containing the url variables in query parameter form if the `GetUrlVariables` API executed without any errors.

**iOS Example**

```csharp
 ACPIdentity.GetUrlVariables(callback => {
   Console.WriteLine("Url variables: " + callback);
 });
```

**Android Example**

```csharp
ACPIdentity.GetUrlVariables(new StringCallback());

class StringCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("Url variables: " + stringContent);
    } 
    else 
    {
      Console.WriteLine("null content in string callback");
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

{% tab title="iOS (AEP 3.x)" %}
#### iOS

{% hint style="info" %}
For iOS AEP libraries, registration is changed to a single API call. Calling the MobileCore.start API is no longer required. See [MobileCore.registerExtensions()](../mobile-core-api-reference.md#registerextension-s) for more information.
{% endhint %}

**Swift**

```swift
// AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([AEPIdentity.Identity.self, Lifecycle.self, Analytics.self], {
        MobileCore.configureWith(appId: "mobilePropertyEnvironmentID")
    })
  ...
}
```

**Objective-C**

```objectivec
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileIdentity.class, AEPMobileLifecycle.class, AEPMobileAnalytics.class] completion:^{
    [AEPMobileCore configureWithAppId: @"mobilePropertyEnvironmentID"];
  }];
  ...
}
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### iOS

Register the Identity extension in your app's `didFinishLaunchingWithOptions` function:

**Swift**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  ACPIdentity.registerExtension()
  // Override point for customization after application launch.
  return true;
}
```

**Objective-C**

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  // Override point for customization after application launch.
  return YES;
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

{% tab title="Xamarin" %}
## C\#

**iOS**

Register the Identity extension in your app's `FinishedLaunching()` function:

```csharp
public override bool FinishedLaunching(UIApplication app, NSDictionary options)
{
  global::Xamarin.Forms.Forms.Init();
  LoadApplication(new App());
    ACPIdentity.RegisterExtension();

  // start core
  ACPCore.Start(startCallback);

  return base.FinishedLaunching(app, options);
}
```

**Android**

Register the Identity extension in your app's `OnCreate()` function:

```csharp
protected override void OnCreate(Bundle savedInstanceState)
{
  base.OnCreate(savedInstanceState);
  global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
  LoadApplication(new App());

  ACPIdentity.RegisterExtension();

  // start core
  ACPCore.Start(new CoreStartCompletionCallback());
}
```
{% endtab %}
{% endtabs %}

## setAdvertisingIdentifier

The advertising ID is preserved between app upgrades, is saved and restored during the standard application backup process, available via the [Signals](../signals) extension, and is removed at uninstall.

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

{% tab title="iOS (AEP 3.x)" %}
### setAdvertisingIdentifier

{% hint style="info" %}
To access IDFA and handle it correctly in your mobile application, see [Apple developer documentation about IDFA](https://developer.apple.com/documentation/adsupport/asidentifiermanager)
{% endhint %}

{% hint style="warning" %}
Starting iOS 14+, applications must use the [App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency) framework to request user authorization before using the Identifier for Advertising (IDFA).
{% endhint %}

#### iOS

**Syntax**

```swift
@objc(setAdvertisingIdentifier:)
public static func setAdvertisingIdentifier(_ identifier: String?)
```

* _identifier_ is a string that provides developers with a simple, standard system to continue to track the Ads through their apps. 

**Example**

**Swift**

```swift
import AdSupport
import AppTrackingTransparency
...

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    ...
    if #available(iOS 14, *) {
       setAdvertisingIdentiferUsingTrackingManager()
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
func setAdvertisingIdentiferUsingTrackingManager() {
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

**Objective-C**

```objectivec
#import <AdSupport/ASIdentifierManager.h>
#import <AppTrackingTransparency/ATTrackingManager.h>
...

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
-   ...
-   
    if (@available(iOS 14, *)) {
        [self setAdvertisingIdentiferUsingTrackingManager];
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

- (void) setAdvertisingIdentiferUsingTrackingManager API_AVAILABLE(ios(14)) {
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

{% tab title="iOS (ACP 2.x)" %}
### setAdvertisingIdentifier

{% hint style="info" %}
To access IDFA and handle it correctly in your mobile application, see [Apple developer documentation about IDFA](https://developer.apple.com/documentation/adsupport/asidentifiermanager)
{% endhint %}

{% hint style="warning" %}
Starting iOS 14+, applications must use the [App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency) framework to request user authorization before using the Identifier for Advertising (IDFA).
{% endhint %}

#### iOS

**Syntax**

```objectivec
+ (void) setAdvertisingIdentifier: (nullable NSString*) adId;
```

* _adId_ is a string that provides developers with a simple, standard system to continue to track the Ads through their apps.    

**Example**

**Swift**

```swift
import AdSupport
import AppTrackingTransparency
...

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    ...
    if #available(iOS 14, *) {
       setAdvertisingIdentiferUsingTrackingManager()
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
            ACPCore.log(ACPMobileLogLevel.debug,
                        tag: "AppDelegateExample",
                        message: "Advertising Tracking is disabled by the user, cannot process the advertising identifier.");
        }
        ACPCore.setAdvertisingIdentifier(idfa);
}

@available(iOS 14, *)
func setAdvertisingIdentiferUsingTrackingManager() {
    ATTrackingManager.requestTrackingAuthorization { (status) in
        var idfa: String = "";

        switch (status) {
        case .authorized:
            idfa = ASIdentifierManager.shared().advertisingIdentifier.uuidString
        case .denied:
            ACPCore.log(.debug,
                        tag: "AppDelegateExample",
                        message: "Advertising Tracking is denied by the user, cannot process the advertising identifier.")
        case .notDetermined:
            ACPCore.log(.debug,
                        tag: "AppDelegateExample",
                        message: "Advertising Tracking is not determined, cannot process the advertising identifier.")
        case .restricted:
            ACPCore.log(.debug,
                        tag: "AppDelegateExample",
                        message: "Advertising Tracking is restricted by the user, cannot process the advertising identifier.")
        }

        ACPCore.setAdvertisingIdentifier(idfa)
    }
}
```

**Objective-C**

```objectivec
#import <AdSupport/ASIdentifierManager.h>
#import <AppTrackingTransparency/ATTrackingManager.h>
...

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
-   ...
-   
    if (@available(iOS 14, *)) {
        [self setAdvertisingIdentiferUsingTrackingManager];
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
        [ACPCore log:ACPMobileLogLevelDebug
                 tag:@"AppDelegateExample"
             message:@"Advertising Tracking is disabled by the user, cannot process the advertising identifier"];
    }
    [ACPCore setAdvertisingIdentifier:idfa];

}

- (void) setAdvertisingIdentiferUsingTrackingManager API_AVAILABLE(ios(14)) {
    [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:
    ^(ATTrackingManagerAuthorizationStatus status){
        NSString *idfa = nil;
        switch(status) {
            case ATTrackingManagerAuthorizationStatusAuthorized:
                idfa = [[[ASIdentifierManager sharedManager] advertisingIdentifier] UUIDString];
                break;
            case ATTrackingManagerAuthorizationStatusDenied:
                [ACPCore log:ACPMobileLogLevelDebug
                         tag:@"AppDelegateExample"
                     message:@"Advertising Tracking is denied by the user, cannot process the advertising identifier"];
                break;
            case ATTrackingManagerAuthorizationStatusNotDetermined:
                [ACPCore log:ACPMobileLogLevelDebug
                         tag:@"AppDelegateExample"
                     message:@"Advertising Tracking is not determined, cannot process the advertising identifier"];
                break;
            case ATTrackingManagerAuthorizationStatusRestricted:
                [ACPCore log:ACPMobileLogLevelDebug
                         tag:@"AppDelegateExample"
                     message:@"Advertising Tracking is restricted by the user, cannot process the advertising identifier"];
                break;
        }

        [ACPCore setAdvertisingIdentifier:idfa];
    }];
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

* _identifier_ _(String)_ provides developers with a simple, standard system to continue to track the Ads through their apps.
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

* _adId_ _(String)_ provides developers with a simple, standard system to continue to track the Ads through their apps.

**Example**

```csharp
ACPCore.SetAdvertisingIdentifier("ADVTID");
```
{% endtab %}

{% tab title="Xamarin" %}
### SetAdvertisingIdentifier

#### C\#

**iOS Syntax**

```csharp
public static void SetAdvertisingIdentifier (string adId);
```

* _adId_ _(String)_ provides developers with a simple, standard system to continue to track the Ads through their apps.

**Android Syntax**

```csharp
public unsafe static void SetAdvertisingIdentifier (string advertisingIdentifier);
```

* _advertisingIdentifier_ _(String)_ provides developers with a simple, standard system to continue to track the Ads through their apps.

**Example**

```csharp
ACPCore.SetAdvertisingIdentifier("ADVTID");
```
{% endtab %}
{% endtabs %}

## setPushIdentifier

This API sets the device token for push notifications in the SDK. If the current SDK privacy status is `optedout`, the push identifier is not set.

{% hint style="info" %}
It is recommended to call `setPushIdentifier` on each application launch to ensure the most up-to-date device token is set to the SDK. If no device token is available, `null`/`nil` should be passed.
{% endhint %}

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

{% tab title="iOS (AEP 3.x)" %}
### setPushIdentifier

#### iOS

```swift
@objc(setPushIdentifier:)
public static func setPushIdentifier(_ deviceToken: Data?)
```

* _deviceToken_  is a string that contains the device token for push notifications.

**Example**

**Swift**

```swift
// Set the deviceToken that the APNs has assigned to the device
MobileCore.setPushIdentifier(deviceToken)
```

**Objective-C**

```objectivec
// Set the deviceToken that the APNS has assigned to the device
[AEPMobileCore setPushIdentifier:deviceToken];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### setPushIdentifier

#### iOS

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

* _deviceToken_  is a string that contains the device token for push notifications.

**Example**

**Swift**

```swift
// Set the deviceToken that the APNs has assigned to the device
ACPCore.setPushIdentifier(deviceToken)
```

**Objective-C**

```objectivec
// Set the deviceToken that the APNS has assigned to the device
[ACPCore setPushIdentifier:deviceToken];
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

The `syncIdentifier()` and `syncIdentifiers()` APIs update the specified customer IDs with the Adobe Experience Cloud ID (ECID) Service.

These APIs synchronize the provided customer identifier type key and value with the authentication state to the ECID Service. If the specified customer ID type exists in the service, this ID type is updated with the new ID and the authentication state. Otherwise, a new customer ID is added.

Starting with _ACPIdentity v2.1.3 (iOS)_ and _Identity v1.1.2 (Android)_ if the new `identifier` value is null or empty, this ID type is removed from the local storage, Identity shared state and not synced with the Adobe ECID Service.

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

* _identifierType (String)_ contains`the identifier type`, and this parameter should not be null or empty.
* _identifier (String)_ contains the `identifier value`, and this parameter should not be null or empty.
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

{% tab title="iOS (AEP 3.x)" %}
#### iOS

**Syntax**

```swift
@objc(syncIdentifierWithType:identifier:authenticationState:)
static func syncIdentifier(identifierType: String, identifier: String, authenticationState: MobileVisitorAuthenticationState)
```

* The _identifierType (String)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier (String)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifierType` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* The _authenticationState (MobileVisitorAuthenticationState)_ value indicates the authentication state for the user and contains one of the following `MobileVisitorAuthenticationState` values:
  * `MobileVisitorAuthenticationState.authenticated`
  * `MobileVisitorAuthenticationState.loggedOut`
  * `MobileVisitorAuthenticationState.unknown`

**Examples**

**Swift**

```swift
Identity.syncIdentifier(identifierType: "idType", 
                            identifier: "idValue", 
                        authentication: .unknown)
```

**Objective-C**

```objectivec
[AEPMobileIdentity syncIdentifierWithType:@"idType"
                               identifier:@"idValue"
                      authenticationState:AEPMobileVisitorAuthStateUnknown];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### iOS

**Syntax**

```objectivec
+ (void) syncIdentifier: (nonnull NSString*) identifierType             
             identifier: (nonnull NSString*) identifier
         authentication: (ADBMobileVisitorAuthenticationState) authenticationState;
```

* The _identifierType (String)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier (String)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifier type` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* The _authenticationState (VisitorIDAuthenticationState)_ value indicates the authentication state for the user and contains one of the following `VisitorID.AuthenticationState` values:
  * `ACPMobileVisitorAuthenticationStateAuthenticated`
  * `ACPMobileVisitorAuthenticationStateLoggedOut`
  * `ACPMobileVisitorAuthenticationStateUnknown`

**Examples**

**Swift**

```swift
ACPIdentity.syncIdentifier("idType", identifier: "idValue", authentication: ACPMobileVisitorAuthenticationState.unknown)
```

**Objective-C**

```objectivec
[ACPIdentity syncIdentifier:@"idType" identifier:@"idValue" authentication:ACPMobileVisitorAuthenticationStateUnknown];
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

**Syntax**

```jsx
syncIdentifier(identifierType: String, identifier: String, authenticationState: string);
```

* The _identifierType (String)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier (String)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifier type` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* _authenticationState (VisitorIDAuthenticationState)_ value indicating authentication state for the user and contains one of the following `VisitorID.AuthenticationState` values:
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

* The _identifierType (String)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier (String)_ contains the `identifier` value, and this parameter should not be null or empty.

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

* The _identifierType (String)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier (String)_ contains the `identifier` value, and this parameter should not be null or empty.

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

* The _identifierType (String)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier (String)_ contains the `identifier` value, and this parameter should not be null or empty.

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

{% tab title="Xamarin" %}
#### C\#

**iOS Syntax**

```csharp
public static void SyncIdentifier (string identifierType, string identifier, ACPMobileVisitorAuthenticationState authenticationState);
```

* The _identifierType (String)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier (String)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifier type` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* _authenticationState_ value indicating authentication state for the user and contains one of the following `ACPMobileVisitorAuthenticationState` values:
  * `ACPMobileVisitorAuthenticationState.Authenticated`
  * `ACPMobileVisitorAuthenticationState.Unknown`
  * `ACPMobileVisitorAuthenticationState.LoggedOut`

**Android Syntax**

```csharp
public unsafe static void SyncIdentifier (string identifierType, string identifier, VisitorID.AuthenticationState authenticationState);
```

* The _identifierType (String)_ contains the `identifier type`, and this parameter should not be null or empty.
* The _identifier (String)_ contains the `identifier` value, and this parameter should not be null or empty.

  If either the `identifier type` or `identifier` contains a null or an empty string, the identifier is ignored by the Identity extension.

* _authenticationState_ value indicating authentication state for the user and contains one of the following `VisitorID.AuthenticationState` values:
  * `VisitorID.AuthenticationState.Authenticated`
  * `VisitorID.AuthenticationState.Unknown`
  * `VisitorID.AuthenticationState.LoggedOut`

**iOS Example**

```csharp
ACPIdentity.SyncIdentifier("idType1", "idValue1", ACPMobileVisitorAuthenticationState.Authenticated);
```

**Android Example**

```csharp
ACPIdentity.SyncIdentifier("idType1", "idValue1", VisitorID.AuthenticationState.Authenticated);
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
Identity.syncIdentifiers(identifiers);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### iOS

**Syntax**

```swift
@objc(syncIdentifiers:)
static func syncIdentifiers(identifiers: [String: String]?)
```

* The _identifiers_ dictionary contains identifier type as the key and identifier as the value, both identifier type and identifier should be non empty and non nil values.

**Examples**

**Swift**

```swift
let ids : [String: String] = ["idType1":"idValue1",
                              "idType2":"idValue2",
                              "idType3":"idValue3"];
Identity.syncIdentifiers(identifiers: ids)
```

**Objective-C**

```objectivec
NSDictionary *ids = @{@"idType1":@"idValue1", 
                      @"idType2":@"idValue2", 
                      @"idType3":@"idValue3"};
[AEPMobileIdentity syncIdentifiers:ids];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### iOS

**Syntax**

```objectivec
+ (void) syncIdentifiers: (nullable NSDictionary*) identifiers;
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

**Examples**

**Swift**

```swift
let identifiers : [String: String] = ["idType1":"idValue1",
                                      "idType2":"idValue2",
                                      "idType3":"idValue3"];
ACPIdentity.syncIdentifiers(identifiers)
```

**Objective-C**

```objectivec
NSDictionary *ids = @{@"idType1":@"idValue1", 
                      @"idType2":@"idValue2", 
                      @"idType3":@"idValue3"};
[ACPIdentity syncIdentifiers:ids];
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
public static void SyncIdentifiers(Dictionary<string, string> identifiers)
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

{% tab title="Xamarin" %}
#### C\#

**iOS Syntax**

```csharp
public static void SyncIdentifiers (NSDictionary identifiers);
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

**Android Syntax**

```csharp
public unsafe static void SyncIdentifiers (IDictionary<string, string> identifiers);
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

**iOS Example**

```csharp
var ids = new NSMutableDictionary<NSString, NSObject>
{
  ["idsType1"] = new NSString("idValue1"),
  ["idsType2"] = new NSString("idValue2"),
  ["idsType3"] = new NSString("idValue3")
};
ACPIdentity.SyncIdentifiers(ids);
```

**Android Example**

```csharp
var ids = new Dictionary<string, string>();
ids.Add("idsType1", "idValue1");
ids.Add("idsType2", "idValue2");
ids.Add("idsType3", "idValue3");
ACPIdentity.SyncIdentifiers(ids);
```
{% endtab %}
{% endtabs %}

## syncIdentifiers (overloaded)

The function of this API is the same as the `syncIdentifier` API. This API passes a list of identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value. In each identifier pair, if the `identifier type` contains a null or an empty string, the identifier is ignored by the Identity extension.

Starting with _ACPIdentity v2.1.3 (iOS)_ and _Identity v1.1.2 (Android)_ if the new `identifier` value is null or empty, this ID type is removed from the local storage, Identity shared state and not synced with the Adobe ECID Service.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers, final VisitorID.AuthenticationState authState)
```

* _identifiers_ is a map that contains IDs with the identifier type as the key, and the string identifier as the value.
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
Identity.syncIdentifiers(identifiers, VisitorID.AuthenticationState.AUTHENTICATED);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### iOS

**Syntax**

```swift
@objc(syncIdentifiers:authenticationState:)
static func syncIdentifiers(identifiers: [String: String]?, authenticationState: MobileVisitorAuthenticationState)
```

* The _identifiers_ dictionary contains identifier type as the key and identifier as the value, both identifier type and identifier should be non empty and non nil values.

* The _authenticationState (MobileVisitorAuthenticationState)_ indicates the authentication state of the user and contains one of the `MobileVisitorAuthenticationState` values:
  * `MobileVisitorAuthenticationState.authenticated`
  * `MobileVisitorAuthenticationState.loggedOut`
  * `MobileVisitorAuthenticationState.unknown`

**Examples**

**Swift**

```swift
let ids : [String: String] = ["idType1":"idValue1",
                              "idType2":"idValue2",
                              "idType3":"idValue3"];
Identity.syncIdentifiers(identifiers: ids, authenticationState: .authenticated)
```

**Objective-C**

```objectivec
NSDictionary *ids = @{@"idType1":@"idValue1", 
                      @"idType2":@"idValue2", 
                      @"idType3":@"idValue3"};
[AEPMobileIdentity syncIdentifiers:ids authenticationState:AEPMobileVisitorAuthStateAuthenticated];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### iOS

**Syntax**

```objectivec
+ (void) syncIdentifiers: (nullable NSDictionary*) identifiers authentication: (ACPMobileVisitorAuthenticationState) authenticationState;
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

* The _authenticationState (VisitorIDAuthenticationState)_ indicates the authentication state of the user and contains one of the `VisitorID.AuthenticationState` values:
  * `ACPMobileVisitorAuthenticationState.AUTHENTICATED`
  * `ACPMobileVisitorAuthenticationState.LOGGED_OUT`
  * `ACPMobileVisitorAuthenticationState.UNKNOWN`

**Examples**

**Swift**

```swift
let ids : [String: String] = ["idType1":"idValue1",
                              "idType2":"idValue2",
                              "idType3":"idValue3"];
ACPIdentity.syncIdentifiers(identifiers, authentication:
ACPMobileVisitorAuthenticationState.authenticated)
```

**Objective-C**

```objectivec
NSDictionary *ids = @{@"idType1":@"idValue1", 
                      @"idType2":@"idValue2", 
                      @"idType3":@"idValue3"};
[ACPIdentity syncIdentifiers:ids authentication:ACPMobileVisitorAuthenticationStateAuthenticated];
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

* The _authenticationState (ACPMobileVisitorAuthenticationState)_ indicates the authentication state of the user and contains one of the `ACPMobileVisitorAuthenticationState` values:
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

* The _authState_ (ACPMobileVisitorAuthenticationState)\_ indicates the authentication state of the user and contains one of the `ACPMobileVisitorAuthenticationState` values:
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

{% tab title="Xamarin" %}
#### C\#

**iOS Syntax**

```csharp
public static void SyncIdentifiers (NSDictionary identifiers, ACPMobileVisitorAuthenticationState authenticationState);
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

* _authenticationState_ value indicating authentication state for the user and contains one of the following `ACPMobileVisitorAuthenticationState` values:
  * `ACPMobileVisitorAuthenticationState.Authenticated`
  * `ACPMobileVisitorAuthenticationState.Unknown`
  * `ACPMobileVisitorAuthenticationState.LoggedOut`

**Android Syntax**

```csharp
public unsafe static void SyncIdentifiers (IDictionary<string, string> identifiers, VisitorID.AuthenticationState authenticationState);
```

* The _identifiers_ dictionary contains identifiers, and each identifier contains an `identifier type` as the key and an `identifier` as the value.

  If any of the identifier pairs contains an empty or null value as the `identifier type`, then it will be ignored.

* _authenticationState_ value indicating authentication state for the user and contains one of the following `VisitorID.AuthenticationState` values:
  * `VisitorID.AuthenticationState.Authenticated`
  * `VisitorID.AuthenticationState.Unknown`
  * `VisitorID.AuthenticationState.LoggedOut`

**iOS Example**

```csharp
var ids = new NSMutableDictionary<NSString, NSObject>
{
  ["idsType1"] = new NSString("idValue1"),
  ["idsType2"] = new NSString("idValue2"),
  ["idsType3"] = new NSString("idValue3")
};
ACPIdentity.SyncIdentifiers(ids, ACPMobileVisitorAuthenticationState.LoggedOut);
```

**Android Example**

```csharp
var ids = new Dictionary<string, string>();
ids.Add("idsType1", "idValue1");
ids.Add("idsType2", "idValue2");
ids.Add("idsType3", "idValue3");
ACPIdentity.SyncIdentifiers(ids, VisitorID.AuthenticationState.LoggedOut);
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

{% tab title="iOS (AEP 3.x)" %}
### iOS (AEP 3.x)

**MobileVisitorAuthenticationState**

This is used to indicate the authentication state for the current `Identifiable`.

```swift
@objc(AEPMobileVisitorAuthState) public enum MobileVisitorAuthenticationState: Int, Codable {
    case unknown = 0
    case authenticated = 1
    case loggedOut = 2
}
```

**Identifiable**

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

{% tab title="iOS (ACP 2.x)" %}
#### iOS (ACP 2.x)

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

{% tab title="Xamarin" %}
#### C\#

**iOS**

**ACPMobileVisitorAuthenticationState**

This is used to indicate the authentication state for the current `ACPMobileVisitorId`.

```csharp
ACPMobileVisitorAuthenticationState.Unknown = 0;
ACPMobileVisitorAuthenticationState.Authenticated = 1;
ACPMobileVisitorAuthenticationState.LoggedOut = 2;
```

**Android**

**VisitorID.AuthenticationState**

This is used to indicate the authentication state for the current `VisitorID`.

```csharp
VisitorID.AuthenticationState.Unknown = 0;
VisitorID.AuthenticationState.Authenticated = 1;
VisitorID.AuthenticationState.LoggedOut = 2;
```
{% endtab %}
{% endtabs %}

