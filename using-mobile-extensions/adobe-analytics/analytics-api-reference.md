# Analytics API reference

## clearQueue <a id="clearqueue"></a>

Force delete, without sending to Analytics, all hits being stored or batched on the SDK.

{% tabs %}
{% tab title="Android" %}

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### Java

**Syntax**

```java
public static void clearQueue()
```

**Example**

```java
Analytics.clearQueue();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### Swift

**Syntax**

```swift
static func clearQueue()
```
**Example**

```swift
Analytics.clearQueue()
```

### Objective-C

**Syntax**

```objectivec
+ (void) clearQueue
```

**Example**

```objectivec
[AEPMobileAnalytics clearQueue];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### Swift

**Syntax**

```swift
static func clearQueue()
```

**Example**

```swift
ACPAnalytics.clearQueue()
```
### Objective-C

**Syntax**

```objectivec
+ (void) clearQueue;
```
**Example**

```objectivec
[ACPAnalytics clearQueue];
```
{% endtab %}

{% tab title="React Native" %}

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### JavaScript

**Syntax**

```jsx
clearQueue();
```

**Example**

```jsx
ACPAnalytics.clearQueue();
```
{% endtab %}

{% tab title="Flutter" %}

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### Dart

**Syntax**

```dart
Future<void> clearQueue();
```

**Example**

```dart
FlutterACPAnalytics.clearQueue();
```
{% endtab %}

{% tab title="Cordova" %}

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### Cordova

**Syntax**

```jsx
ACPAnalytics.clearQueue = function(success, fail);
```

* _success_ is a callback containing a general success message if the clearQueue API executed without any errors.
* _fail_ is a callback containing error information if the clearQueue API was executed with errors.

**Example**

```jsx
ACPAnalytics.clearQueue(function (handleCallback) {
  console.log("AdobeExperienceSDK: Clear queued hits successful. " + handleCallback);
} ,function (handleError) {
  console.log("AdobeExperenceSDK: Failed to clear queued hits: " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### C\#

**Syntax**

```csharp
public static void ClearQueue()
```

**Example**

```csharp
ACPAnalytics.ClearQueue();
```
{% endtab %}

{% tab title="Xamarin" %}

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### C\#

**Syntax**

```csharp
public static void ClearQueue ();
```

**Example**

```csharp
ACPAnalytics.ClearQueue();
```
{% endtab %}
{% endtabs %}

## extensionVersion <a id="extensionversion"></a>

The `extensionVersion()` API returns the version of the Analytics extension that is registered with the Mobile Core extension.

To get the version of the Analytics extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
### Java

```java
String analyticsExtensionVersion = Analytics.extensionVersion();
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
let version = Analytics.extensionVersion
```
### Objective-C

**Syntax**

```objectivec
+ (nonnull NSString*) extensionVersion;
```
**Examples**

```objectivec
NSString *version = [AEPMobileAnalytics extensionVersion];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static func extensionVersion()
```
**Examples**
```swift
let analyticsExtensionVersion  = ACPAnalytics.extensionVersion()
```

### Objective-C

**Syntax**

```objectivec
+ (nonnull NSString*) extensionVersion;
```

**Examples**
```objectivec
NSString *analyticsExtensionVersion = [ACPAnalytics extensionVersion];
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
ACPAnalytics.extensionVersion().then(analyticsExtensionVersion => console.log("AdobeExperienceSDK: ACPAnalytics version: " + analyticsExtensionVersion));
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

```dart
String analyticsExtensionVersion = await FlutterACPAnalytics.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

```jsx
ACPAnalytics.extensionVersion(function(version) {  
   console.log("ACPAnalytics version: " + version);
}, function(error) {  
   console.log(error);  
});
```
{% endtab %}

{% tab title="Unity" %}
### C\#

```csharp
string analyticsExtensionVersion = ACPAnalytics.ExtensionVersion();
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

```csharp
string analyticsExtensionVersion = ACPAnalytics.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

## getQueueSize <a id="getqueuesize"></a>

Retrieves the total number of Analytics hits in the tracking queue.

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
 public static void getQueueSize(final AdobeCallback<Long> callback)
```

* _callback_ is invoked with the queue size value. When an AdobeCallbackWithError is provided, an AdobeError can be returned in the eventuality of an unexpected error or if the default timeout \(5000ms\) is met before the callback is returned with queue size.

**Example**

```java
Analytics.getQueueSize(new AdobeCallback<Long>() {
    @Override
    public void call(final Long queueSize) {
        // handle the queueSize
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

Please use the [getQueueSizeWithCompletionHandler](analytics-api-reference.md#getqueuesizewithcompletionhandler) API instead.
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static func getQueueSize(_ callback: @escaping (UInt) -> Void)
```

**Example**

```swift
ACPAnalytics.getQueueSize { (queueSize) in    
     // handle queue size   
}
```

### Objective-C

**Syntax**

```objectivec
+ (void) getQueueSize: (nonnull void (^) (NSUInteger queueSize)) callback;
```

* _callback_ is invoked with the queue size value.

**Example**


```objectivec
[ACPAnalytics getQueueSize: ^(NSUInteger queueSize) {    
    // handle queue size
}];
```
{% endtab %}

{% tab title="React Native" %}

### JavaScript

**Syntax**

```jsx
getQueueSize(): Promise<?integer>;
```

**Example**

```jsx
ACPAnalytics.getQueueSize().then(size => console.log("AdobeExperienceSDK: Queue size: " + size));
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

**Syntax**

```dart
Future<int> getQueueSize;
```

**Example**

```dart
int queueSize;

try {
    queueSize = await FlutterACPAnalytics.queueSize;
} on PlatformException {
    log("Failed to get the queue size");
}
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

**Syntax**

```jsx
ACPAnalytics.getQueueSize = function(success, fail);
```

* _success_ is a callback containing the `queue size` if the getQueueSize API executed without any errors.
* _fail_ is a callback containing error information if the getQueueSize API was executed with errors.

**Example**

```csharp
ACPAnalytics.getQueueSize(function (handleCallback) {
  console.log("AdobeExperienceSDK: Queue size: " + handleCallback);
} ,function (handleError) {
  console.log("AdobeExperenceSDK: Failed to get queue size: " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
### C\#

**Syntax**

```csharp
public static void GetQueueSize(AdobeGetQueueSizeCallback callback)
```

* _callback_ is a callback containing the `queue size` if the GetQueueSize API executed without any errors.

**Example**

```csharp
[MonoPInvokeCallback(typeof(AdobeGetQueueSizeCallback))]
public static void HandleAdobeGetQueueSizeCallback(long queueSize)
{
    Debug.Log("Queue size is : " + queueSize);
}
ACPAnalytics.GetQueueSize(HandleAdobeGetQueueSizeCallback);
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

**syntax**

```csharp
public unsafe static void GetQueueSize (Action<nuint> callback);
```

* _callback_ is a callback containing the `queue size` if the GetQueueSize API executed without any errors.

**example**

```csharp
ACPAnalytics.GetQueueSize(callback => {
  Console.WriteLine("Queue size: " + callback);
});
```
### Android

**syntax**

```csharp
public unsafe static void GetQueueSize (IAdobeCallback callback);
```

* _callback_ is a callback containing the `queue size` if the GetQueueSize API executed without any errors.

**example**

```csharp
ACPAnalytics.GetQueueSize(new StringCallback());

class StringCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("Queue size: " + stringContent);
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

## getQueueSizeWithCompletionHandler <a id="getqueuesizewithcompletionhandler"></a>

Retrieves the total number of Analytics hits in the tracking queue. Invoke the callback with NSError if an unexpected error occurs or the request times out.

{% tabs %}
{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static func getQueueSize(completion: @escaping (Int, Error?) -> Void)
```

**Example**

```swift
Analytics.getQueueSize { (queueSize, error) in
    // Handle error (if non-nil) or use queueSize.
}
```
### Objective-C

**Syntax**

```objectivec
+ (void)getQueueSize:^(NSInteger, NSError * _Nullable)completion
```

**Example**

```objectivec
[AEPMobileAnalytics getQueueSize:^(NSInteger queueSize, NSError * _Nullable error) {
    // Handle error (if non-nil) or use queueSize.
 }];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static func getQueueSize(completionHandler: @escaping (UInt, Error?) -> Void)
```
**Example**

```swift
ACPAnalytics.getQueueSizeWithCompletionHandler { (queueSize, error) in    
    // Handle error (if non-nil) or use queueSize.  
}
```
### Objective-C

**Syntax**

```objectivec
+ (void) getQueueSizeWithCompletionHandler: (nonnull void (^) (NSUInteger queueSize, NSError* __nullable error)) completionHandler;
```

* _completionHandler_ is invoked with the queue size value or an NSError if an unexpected error occurs or the request times out.

**Example**

```objectivec
[ACPAnalytics getQueueSizeWithCompletionHandler: ^(NSUInteger queueSize, NSError * _Nullable error) {    
    // Handle error (if non-nil) or use queueSize.
}];
```
{% endtab %}
{% endtabs %}

## getTrackingIdentifier <a id="gettrackingidentifier"></a>

Retrieves the Analytics tracking identifier that is generated for this app/device instance. This identifier is an app-specific, unique visitor ID that is generated at the initial launch and is stored and used after the initial launch. The ID is preserved between app upgrades and is removed when the app is uninstalled as well as on [MobileCore.resetIdentities](analytics-api-reference.md#resetidentities) API call or on privacy status opt out.

{% hint style="warning" %}
Starting with v1.2.9 (Android) / v3.0.3(iOS AEPAnalytics) / v2.5.1 (iOS ACPAnalytics) this API does not generate or retrieve a new tracking identifier (AID) for new visitors. For the visitors which have an AID previously generated will continue retrieve the AID value with this API, and new users will use the ECID (MID) value as the primary identity.
Before using this API, see the documentation on identifying [unique visitors](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}

### Java
Retrieves the Analytics tracking identifier.

**Syntax**

```java
 public static void
   getTrackingIdentifier(final AdobeCallback<String> callback)
```

* _callback_ is invoked with the tracking Identifier string value. When an AdobeCallbackWithError is provided, an AdobeError can be returned in the eventuality of an unexpected error or if the default timeout \(5000ms\) is met before the callback is returned with analytics tracking identifier.

**Example**

```java
Analytics.getTrackingIdentifier(new AdobeCallback<String>() {
    @Override
    public void call(final String trackingIdentifier) {
        // check the trackingIdentifier value    
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

Retrieves the Analytics tracking identifier. See [getTrackingIdentifierWithCompletionHandler](analytics-api-reference.md#gettrackingidentifierwithcompletionhandler)
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

Retrieves the Analytics tracking identifier.

### Swift

**Syntax**

```swift
static func getTrackingIdentifier(_ callback: @escaping (String?) -> Void)
```

**Example**

```swift
ACPAnalytics.getTrackingIdentifier { (trackingIdentifier) in
    // check the trackingIdentifier value  
}
```
### Objective-C

**Syntax**

```objectivec
+ (void) getTrackingIdentifier: (nonnull void (^) (NSString* __nullable trackingIdentifier)) callback;
```

* _callback_ is invoked with the tracking Identifier string value.

**Example**

```objectivec
[ACPAnalytics getTrackingIdentifier:^(NSString * _Nullable trackingIdentifier) {
    // check the trackingIdentifier value  
}];
```
{% endtab %}

{% tab title="React Native" %}

### JavaScript

Retrieves the Analytics tracking identifier.

**Syntax**

```jsx
getTrackingIdentifier();
```

* _callback_ is invoked with the tracking Identifier string value.

**Example**

```jsx
ACPAnalytics.getTrackingIdentifier().then(identifier => console.log("AdobeExperienceSDK: Tracking identifier: " + identifier));
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

Retrieves the Analytics tracking identifier.

**Syntax**

```dart
Future<String> getTrackingIdentifier;
```

**Example**

```dart
String trackingId;

try {
    trackingId = await FlutterACPAnalytics.trackingIdentifier;
} on PlatformException {
    log("Failed to get the tracking identifier");
}
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

Retrieves the Analytics tracking identifier.

```jsx
ACPAnalytics.getTrackingIdentifier = function(success, fail);
```

* _success_ is a callback containing the tracking Identifier string value.
* _fail_ is a callback containing error information if the getTrackingIdentifier API was executed with errors.

**Example**

```jsx
ACPAnalytics.getTrackingIdentifier(function (handleCallback) {
  console.log("AdobeExperienceSDK: Retrieved tracking identifier: " + handleCallback);
} ,function (handleError) {
  console.log("AdobeExperenceSDK: Failed to retrieve tracking identifier: " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
### C\#

Retrieves the Analytics tracking identifier.

```csharp
public static void GetTrackingIdentifier(AdobeGetTrackingIdentifierCallback callback)
```

* _callback_ is a callback containing the tracking Identifier string value.

**Example**

```csharp
[MonoPInvokeCallback(typeof(AdobeGetTrackingIdentifierCallback))]
public static void HandleAdobeGetTrackingIdentifierCallback(string trackingIdentifier)
{
    Debug.Log("Tracking identifier is : " + trackingIdentifier);
}
ACPAnalytics.GetTrackingIdentifier(HandleAdobeGetTrackingIdentifierCallback);
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

Retrieves the Analytics tracking identifier.

**syntax**

```csharp
public unsafe static void GetTrackingIdentifier (Action<NSString> callback);
```

* _callback_ is a callback containing the tracking Identifier string value.

**example**

```csharp
ACPAnalytics.GetTrackingIdentifier(callback => {
  Console.WriteLine("Tracking identifier: " + callback);
});
```
### Android

**syntax**

```csharp
public unsafe static void GetTrackingIdentifier (IAdobeCallback callback);
```

* _callback_ is a callback containing the tracking Identifier string value.

**example**

```csharp
ACPAnalytics.GetTrackingIdentifier(new StringCallback());

class StringCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("Tracking identifier: " + stringContent);
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

## getTrackingIdentifierWithCompletionHandler <a id="gettrackingidentifierwithcompletionhandler"></a>

{% hint style="warning" %}
Starting with v1.2.9 (Android) / v3.0.3(iOS AEPAnalytics) / v2.5.1 (iOS ACPAnalytics) this API does not generate or retrieve a new tracking identifier (AID) for new visitors. For the visitors which have an AID previously generated will continue retrieve the AID value with this API, and new users will use the ECID (MID) value as the primary identity.
Before you use this API, please read the documentation on [identifying unique visitors](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html).
{% endhint %}

Retrieves the Analytics tracking identifier that is generated for this app/device instance. This identifier is an app-specific, unique visitor ID that is generated at the initial launch and is stored and used after the initial launch. The ID is preserved between app upgrades and is removed when the app is uninstalled as well as on [MobileCore.resetIdentities](analytics-api-reference.md#resetidentities) API call or on privacy status opt out. Invoke the callback with NSError if an unexpected error occurs or the request times out.

{% hint style="info" %}
If you have an [Experience Cloud ID](https://app.gitbook.com/@aep-sdks/s/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#getexperiencecloudid) and have not yet configured a visitor ID grace period, the value returned by `getTrackingIdentifier` might be null.
{% endhint %}

{% tabs %}
{% tab title="iOS (AEP 3.x)" %}

Retrieves the Analytics tracking identifier.

### Swift

**Syntax**

```swift
static func getTrackingIdentifier(completion: @escaping (String?, Error?) -> Void)
```

**Example**

```swift
Analytics.getTrackingIdentifier { (trackingId, error) in
   // Handle the error (if non-nil) or use the trackingIdentifier value
}
```
### Objective-C

**Syntax**

```objectivec
+ (void) getTrackingIdentifier:^(NSString * _Nullable, NSError * _Nullable)completion
```

**Example**
```objectivec
AEPMobileAnalytics getTrackingIdentifier:^(NSString * _Nullable trackingIdentifier, NSError * _Nullable error) {
   // Handle the error (if non-nil) or use the trackingIdentifier value
}];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static func getTrackingIdentifier(completionHandler: @escaping (String?, Error?) -> Void)
```

* _completionHandler_ is invoked with the tracking Identifier string value. or an NSError if an unexpected error occurs or the request times out.

**Example**

```swift
ACPAnalytics.getTrackingIdentifierWithCompletionHandler { (trackingIdentifier, error) in    
     // Handle the error (if non-nil) or use the trackingIdentifier value.
}
```
### Objective-C

**Syntax**

```objectivec
+ (void) getTrackingIdentifierWithCompletionHandler: (nonnull void (^) (NSString* __nullable trackingIdentifier, NSError* __nullable error)) completionHandler;
```

**Example**

```objectivec
[ACPAnalytics getTrackingIdentifierWithCompletionHandler:^(NSString * _Nullable trackingIdentifier, NSError * _Nullable error) {
    // Handle the error (if non-nil) or use the trackingIdentifier value.
}];
```
{% endtab %}
{% endtabs %}

## getVisitorIdentifier <a id="getvisitoridentifier"></a>

{% hint style="warning" %}
Before using this API, see [Identify unique visitors](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html).
{% endhint %}

This API gets a custom Analytics visitor identifier, which has been set previously using [setVisitorIdentifier](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#setvisitoridentifier).

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
public static void getVisitorIdentifier(AdobeCallback<String> callback)
```

* _callback_ is invoked with the visitor identifier value. When an AdobeCallbackWithError is provided, an AdobeError can be returned in the eventuality of an unexpected error or if the default timeout \(5000ms\) is met before the callback is returned with visitor identifier.

**Example**

```java
Analytics.getVisitorIdentifier(new AdobeCallback<String>() {
    @Override
    public void call(final String visitorIdentifier) {
        // check the visitorIdentifier value    
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

See [getVisitorIdentifierWithCompletionHandler](analytics-api-reference.md#getvisitoridentifierwithcompletionHandler)
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static func getVisitorIdentifier(_ callback: @escaping (String?) -> Void)
```
* _callback_ is invoked with the visitor identifier value.

**Example**

```swift
ACPAnalytics.getVisitorIdentifier { (visitorIdentifier) in
    // check the visitorIdentifier value  
}
```
### Objective-C

**Syntax**

```objectivec
+ (void) getVisitorIdentifier: (nonnull void (^) (NSString* __nullable visitorIdentifier)) callback;
```

**Example**
```objectivec
[ACPAnalytics getVisitorIdentifier:^(NSString * _Nullable visitorIdentifier) {
    // check the visitorIdentifier value   
}];
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Syntax**

```jsx
getVisitorIdentifier();
```

**Example**

```jsx
ACPAnalytics.getVisitorIdentifier().then(vid => console.log("AdobeExperienceSDK: Visitor identifier: " + vid));
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

**Syntax**

```dart
Future<String> visitorIdentifier;
```

**Example**

```dart
String visitorId;

try {
    visitorId = await FlutterACPAnalytics.visitorIdentifier;
} on PlatformException {
    visitorId = "Failed to get the visitor identifier";
}
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

**Syntax**

```jsx
ACPAnalytics.getVisitorIdentifier = function(success, fail);
```

* _success_ is a callback containing the `Visitor Identifier` string if the getVisitorIdentifier API executed without any errors.
* _fail_ is a callback containing error information if the getVisitorIdentifier API was executed with errors.

**Example**

```jsx
ACPAnalytics.getVisitorIdentifier(function (handleCallback) {
  console.log("AdobeExperienceSDK: Retrieved custom visitor identifier: " + handleCallback);
} ,function (handleError) {
  console.log("AdobeExperenceSDK: Failed to retrieve custom visitor identifier: " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
### C\#

**Syntax**

```csharp
public static void GetVisitorIdentifier(AdobeGetVisitorIdentifierCallback callback)
```

* _callback_ is a callback containing the `Visitor Identifier` string if the GetVisitorIdentifier API executed without any errors.

**Example**

```csharp
[MonoPInvokeCallback(typeof(AdobeGetVisitorIdentifierCallback))]
public static void HandleAdobeGetVisitorIdentifierCallback(string visitorIdentifier)
{
    Debug.Log("Visitor identifier is : " + visitorIdentifier);
}
ACPAnalytics.GetVisitorIdentifier(HandleAdobeGetVisitorIdentifierCallback);
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

**syntax**

```csharp
public unsafe static void GetVisitorIdentifier (Action<NSString> callback);
```

* _callback_ is a callback containing the visitor Identifier string value.

**example**

```csharp
ACPAnalytics.GetVisitorIdentifier(callback => {
  Console.WriteLine("Visitor identifier: " + callback);
});
```

**syntax**

```csharp
public unsafe static void GetVisitorIdentifier (IAdobeCallback callback);
```

* _callback_ is a callback containing the visitor Identifier string value.

**example**

```csharp
ACPAnalytics.GetVisitorIdentifier(new StringCallback());

class StringCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("Visitor identifier: " + stringContent);
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

## getVisitorIdentifierWithCompletionHandler <a id="getvisitoridentifierwithcompletionhandler"></a>

{% hint style="warning" %}
Before using this API, see [Identify unique visitors](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html).
{% endhint %}

This API gets a custom Analytics visitor identifier, which has been set previously using [setVisitorIdentifier](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#setvisitoridentifier). Callback with NSError if an unexpected error occurs or the request times out.

{% tabs %}
{% tab title="iOS (AEP 3.x)" %}
### getVisitorIdentifier

### Swift

**Syntax**

```swift
static func getVisitorIdentifier(completion: @escaping (String?, Error?) -> Void)
```
**Example**

```swift
Analytics.getVisitorIdentifier { (visitorIdentifier, error) in
   // Handle the error (if non-nil) or use the visitorIdentifier value
}
```

### Objective-C

**Syntax**

```objectivec
+ (void) getVisitorIdentifier:^(NSString * _Nullable, NSError * _Nullable)completion
```

**Example**
```objectivec
[AEPMobileAnalytics getVisitorIdentifier:^(NSString * _Nullable visitorIdentifier, NSError * _Nullable error) {
   // Handle the error (if non-nil) or use the visitorIdentifier value
}];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static func getVisitorIdentifier(completionHandler: @escaping (String?, Error?) -> Void)
```
* _completionHandler_ is invoked with the visitor identifier value or an NSError if an unexpected error occurs or the request times out.

**Example**
```swift
ACPAnalytics.getVisitorIdentifierWithCompletionHandler { (visitorIdentifier, error) in
    // Handle the error (if non-nil) or use the visitorIdentifier value
}
```
### Objective-C

**Syntax**

```text
+ (void) getVisitorIdentifierWithCompletionHandler: (nonnull void (^) (NSString* __nullable visitorIdentifier, NSError* __nullable error)) completionHandler;
```
**Example**
```text
[ACPAnalytics getVisitorIdentifierWithCompletionHandler:^(NSString * _Nullable visitorIdentifier, NSError * _Nullable error) {
    // Handle the error (if non-nil) or use the visitorIdentifier value
}];
```
{% endtab %}
{% endtabs %}

## resetIdentities

Clears the identities stored in the Analytics extension - `tracking identifier (AID)` and the `custom visitor identifiers (VID)` stored in the Analytics extension and force deletes, without sending to Analytics, all hits being stored or batched on the SDK.


{% hint style="info" %}
Support for this API was added in:

* Android Analytics version 1.2.9

* iOS AEPAnalytics version 3.0.3

{% endhint %}

See [MobileCore.resetIdentities](../../foundation-extensions/mobile-core/mobile-core-api-reference.md#resetidentities) for more details.

## sendQueuedHits <a id="sendqueuedhits"></a>

Sends all queued hits to Analytics, regardless of the current hit batch settings.

{% tabs %}
{% tab title="Android" %}

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### Java

**Syntax**

```java
public static void sendQueuedHits()
```

**Example**

```java
Analytics.sendQueuedHits();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### Swift

**Syntax**

```swift
static func sendQueuedHits()
```

**Example**

```swift
[AEPMobileAnalytics sendQueueHits];
```
### Objective-C

**Syntax**

```objectivec
+ (void) sendQueueHits
```
**Example**

```objectivec
Analytics.sendQueuedHits()
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

### Swift

**Syntax**

```swift
static func sendQueuedHits()
```
**Example**

```swift
ACPAnalytics.sendQueuedHits()
```
### Objective-C

**Syntax**

```objectivec
+ (void) sendQueuedHits;
```
**Example**

```objectivec
[ACPAnalytics sendQueuedHits];
```
{% endtab %}

{% tab title="React Native" %}

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

### JavaScript

**Syntax**

```jsx
sendQueuedHits();
```

**Example**

```jsx
ACPAnalytics.sendQueuedHits();
```
{% endtab %}

{% tab title="Flutter" %}

### Dart

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

**Syntax**

```dart
Future<void> sendQueuedHits();
```

**Example**

```dart
FlutterACPAnalytics.sendQueuedHits();
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

**Syntax**

```jsx
ACPAnalytics.sendQueuedHits = function(success, fail);
```

* _success_ is a callback containing a general success message if the sendQueuedHits API executed without any errors.
* _fail_ is a callback containing error information if the sendQueuedHits API was executed with errors.

**Example**

```jsx
ACPAnalytics.sendQueuedHits(function (handleCallback) {
  console.log("AdobeExperienceSDK: Send queued hits successful. " + handleCallback);
} ,function (handleError) {
  console.log("AdobeExperenceSDK: Failed to send queued hits: " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
### C\#

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

**Syntax**

```csharp
public static void SendQueuedHits()
```

**Example**

```csharp
ACPAnalytics.SendQueuedHits();
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

**Syntax**

```csharp
public static void SendQueuedHits ();
```

**Example**

```csharp
ACPAnalytics.SendQueuedHits();
```
{% endtab %}
{% endtabs %}

## setVisitorIdentifier <a id="setvisitoridentifier"></a>

{% hint style="warning" %}
Before using this API, see [Identify unique visitors](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html).
{% endhint %}

Sets a custom Analytics visitor identifier. For more information, see [Custom Visitor ID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html).

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
 public static void setVisitorIdentifier(final String visitorIdentifier)
```

* _visitorIdentifier_ is the new value for the visitor identifier.

**Example**

```java
Analytics.setVisitorIdentifier("custom_identifier");
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static func setVisitorIdentifier(visitorIdentifier: String)
```

* _visitorIdentifier_ is the new value for the visitor identifier.

**Example**

```swift
Analytics.setVisitorIdentifier(visitorIdentifier:"custom_identifier")
```

### Objective-C

**Syntax**

```objectivec
+ (void) setVisitorIdentifier:(NSString * _Nonnull)
```
**Example**
```objectivec
[AEPMobileAnalytics setVisitorIdentifier:@"custom_identifier"];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static func setVisitorIdentifier(_ visitorIdentifier: String)
```

* _visitorIdentifier_ is the new value for the visitor identifier.

**Example**

```swift
ACPAnalytics.setVisitorIdentifier("custom_identifier")
```

### Objective-C

**Syntax**

```objectivec
+ (void) setVisitorIdentifier: (nonnull NSString*) visitorIdentifier;
```

**Example**
```objectivec
[ACPAnalytics setVisitorIdentifier:@"custom_identifier"];
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Syntax**

```jsx
setVisitorIdentifier(visitorIdentifier);
```

* _visitorIdentifier_ is the new value for the visitor identifier.

**Example**

```jsx
ACPAnalytics.setVisitorIdentifier("custom_identifier");
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

**Syntax**

```dart
Future<void> setVisitorIdentifier(visitorIdentifier);
```

* _visitorIdentifier_ is the new value for the visitor identifier.

**Example**

```dart
FlutterACPAnalytics.setVisitorIdentifier("yourVisitorId");
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

**Syntax**

```jsx
ACPAnalytics.setVisitorIdentifier(visitorIdentifier, success, fail);
```

* _visitorIdentifier_ is the new value for the visitor identifier.
* _success_ is a callback containing a general success message if the setVisitorIdentifier API executed without any errors.
* _fail_ is a callback containing error information if the setVisitorIdentifier API was executed with errors.

**Example**

```jsx
ACPAnalytics.setVisitorIdentifier("custom_identifier", function (handleCallback) {
  console.log("AdobeExperienceSDK: Custom visitor identifier set successfully. " + handleCallback);
} ,function (handleError) {
  console.log("AdobeExperenceSDK: Failed to set custom visitor identifier: " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
### C\#

**Syntax**

```csharp
public static void SetVisitorIdentifier(string visitorId)
```

* _visitorId_ is the new value for the visitor identifier.

**Example**

```csharp
ACPAnalytics.SetVisitorIdentifier("VisitorIdentifier");
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

**syntax**

```csharp
public static void SetVisitorIdentifier (string visitorIdentifier);
```

* _visitorIdentifier_ is the new value for the visitor identifier.

### Android

**syntax**

```csharp
public unsafe static void SetVisitorIdentifier (string visitorID);
```

* _visitorID_ is the new value for the visitor identifier.

**Example**

```csharp
ACPAnalytics.SetVisitorIdentifier("VisitorIdentifier");
```
{% endtab %}
{% endtabs %}
