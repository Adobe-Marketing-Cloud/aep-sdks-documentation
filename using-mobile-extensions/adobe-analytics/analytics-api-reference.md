# Analytics API reference

## Version of the Analytics extension

The `extensionVersion()` API returns the version of the Analytics extension that is registered with the Mobile Core extension.

To get the version of the Analytics extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}

#### Java

```java
String analyticsExtensionVersion = Analytics.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

**Swift**

```swift
let version = Analytics.extensionVersion
```

**Objective-C**

```objectivec
NSString *version = [AEPMobileAnalytics extensionVersion];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

```objectivec
NSString *analyticsExtensionVersion = [ACPAnalytics extensionVersion];
```

**Swift**

```swift
let analyticsExtensionVersion  = ACPAnalytics.extensionVersion()
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

## clearQueue <a id="clearqueue"></a>

Force delete, without sending to Analytics, all hits being stored or batched on the SDK.

{% tabs %}
{% tab title="Android" %}
### clearQueue

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

#### Syntax

```java
public static void clearQueue()
```

#### Example

```java
Analytics.clearQueue();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### clearQueue

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

#### Syntax

```swift
static func clearQueue()
```

#### Example

#### Swift

```swift
Analytics.clearQueue()
```

#### Objective-C

```objectivec
[AEPMobileAnalytics clearQueue];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### clearQueue

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

#### Syntax

```objectivec
+ (void) clearQueue;
```

#### Example

#### Objective-C

```objectivec
[ACPAnalytics clearQueue];
```

#### Swift

```swift
ACPAnalytics.clearQueue()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### clearQueue

**Syntax**

```jsx
clearQueue();
```

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

**Example**

```jsx
ACPAnalytics.clearQueue();
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

### clearQueue

**Syntax**

```dart
Future<void> clearQueue();
```

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

**Example**

```dart
FlutterACPAnalytics.clearQueue();
```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

### clearQueue

```jsx
ACPAnalytics.clearQueue = function(success, fail);
```

* _success_ is a callback containing a general success message if the clearQueue API executed without any errors.
* _fail_ is a callback containing error information if the clearQueue API was executed with errors.

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

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
#### C\#

### ClearQueue

```csharp
public static void ClearQueue()
```

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

**Example**

```csharp
ACPAnalytics.ClearQueue();
```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

### ClearQueue

```csharp
public static void ClearQueue ();
```

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

**Example**

```csharp
ACPAnalytics.ClearQueue();
```
{% endtab %}
{% endtabs %}

## getQueueSize <a id="getqueuesize"></a>

Retrieves the total number of Analytics hits in the tracking queue.

{% tabs %}
{% tab title="Android" %}
### getQueueSize

#### Syntax

```java
 public static void getQueueSize(final AdobeCallback<Long> callback)
```

* _callback_ is invoked with the queue size value. When an AdobeCallbackWithError is provided, an AdobeError can be returned in the eventuality of an unexpected error or if the default timeout \(5000ms\) is met before the callback is returned with queue size.

#### Example

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

### getQueueSize

#### Syntax

```swift
static func getQueueSize(completion: @escaping (Int, Error?) -> Void)
```

#### Example

**Swift**

```swift
Analytics.getQueueSize { (queueSize, _) in
    // handle queue size 
}
```

**Objective-C**

```objectivec
[AEPMobileAnalytics getQueueSize:^(NSInteger queueSize, NSError * _Nullable error) {
    // handle queue size
 }];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### getQueueSize

#### Syntax

```objectivec
+ (void) getQueueSize: (nonnull void (^) (NSUInteger queueSize)) callback;
```

* _callback_ is invoked with the queue size value.

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPAnalytics getQueueSize: ^(NSUInteger queueSize) {    
    // use queue size
}];
```

**Swift**

```swift
ACPAnalytics.getQueueSize { (queueSize) in    
     // use queue size   
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### getQueueSize

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
#### Dart

### getQueueSize

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
#### Cordova

### getQueueSize

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
#### C\#

### GetQueueSize

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
#### C\#

### GetQueueSize

**iOS Syntax**

```csharp
public unsafe static void GetQueueSize (Action<nuint> callback);
```

* _callback_ is a callback containing the `queue size` if the GetQueueSize API executed without any errors.

**iOS Example**

```csharp
ACPAnalytics.GetQueueSize(callback => {
  Console.WriteLine("Queue size: " + callback);
});
```

**Android Syntax**

```csharp
public unsafe static void GetQueueSize (IAdobeCallback callback);
```

* _callback_ is a callback containing the `queue size` if the GetQueueSize API executed without any errors.

**Android Example**

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

## getQueueSizeWithCompletionHandler <a id="getQueueSizeWithCompletionHandler"></a>

Retrieves the total number of Analytics hits in the tracking queue. Invoke the callback with NSError if unexpected error occures or request times out.

{% tabs %}
{% tab title="iOS (ACP 2.x)" %}

### getQueueSizeWithCompletionHandler

#### Syntax

```objectivec
+ (void) getQueueSizeWithCompletionHandler: (nonnull void (^) (NSUInteger queueSize, NSError* __nullable error)) completionHandler;
```

* _completionHandler_ is invoked with the queue size value or an NSError if an unexpected error occurs or the request times out.

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPAnalytics getQueueSizeWithCompletionHandler: ^(NSUInteger queueSize, NSError * _Nullable error) {    
    // use queue size or handle error
}];
```

**Swift**

```swift
ACPAnalytics.getQueueSizeWithCompletionHandler { (queueSize, error) in    
     // use queue size or handle error  
}
```
{% endtab %}
{% endtabs %}

## getTrackingIdentifier <a id="gettrackingidentifier"></a>

{% hint style="warning" %}
Before you use this API, see [Identify unique visitors](https://docs.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-overview.html).
{% endhint %}

Retrieves the Analytics tracking identifier that is generated for this app/device instance. This identifier is an app-specific, unique visitor ID that is generated at the initial launch and is stored and used after the initial launch. The ID is preserved between app upgrades and is removed when the app is uninstalled.

{% hint style="info" %}
If you have an [Experience Cloud ID](https://app.gitbook.com/@aep-sdks/s/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#get-experience-cloud-ids), and have not yet configured a visitor ID grace period, the value returned by `getTrackingIdentifier` might be null.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### getTrackingIdentifier

Retrieves the Analytics tracking identifier.

#### Syntax

```java
 public static void
   getTrackingIdentifier(final AdobeCallback<String> callback)
```

* _callback_ is invoked with the tracking Identifier string value. When an AdobeCallbackWithError is provided, an AdobeError can be returned in the eventuality of an unexpected error or if the default timeout \(5000ms\) is met before the callback is returned with analytics tracking identifier.

#### **Example**

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

### getTrackingIdentifier

Retrieves the Analytics tracking identifier.

#### Syntax

```swift
+ (void) getTrackingIdentifier: (nonnull void (^) (NSString* __nullable trackingIdentifier)) callback;
```

#### Example

**Swift**

```swift
Analytics.getTrackingIdentifier { (trackingId, _) in
   // check the trackingIdentifier value  
}
```

**Objective-C**

```objectivec
AEPMobileAnalytics getTrackingIdentifier:^(NSString * _Nullable trackingIdentifier, NSError * _Nullable error) {
   // check the trackingIdentifier value  
}];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### getTrackingIdentifier

Retrieves the Analytics tracking identifier.

#### Syntax

```objectivec
+ (void) getTrackingIdentifier: (nonnull void (^) (NSString* __nullable trackingIdentifier)) callback;
```

* _callback_ is invoked with the tracking Identifier string value.

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPAnalytics getTrackingIdentifier:^(NSString * _Nullable trackingIdentifier) {
    // check the trackingIdentifier value  
}];
```

**Swift**

```swift
ACPAnalytics.getTrackingIdentifier { (trackingIdentifier) in
    // check the trackingIdentifier value  
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### getTrackingIdentifier

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
#### Dart

### getTrackingIdentifier

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
#### Cordova

### getTrackingIdentifier

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
#### C\#

### GetTrackingIdentifier

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
#### C\#

### GetTrackingIdentifier

Retrieves the Analytics tracking identifier.

**iOS Syntax**

```csharp
public unsafe static void GetTrackingIdentifier (Action<NSString> callback);
```

* _callback_ is a callback containing the tracking Identifier string value.

**iOS Example**

```csharp
ACPAnalytics.GetTrackingIdentifier(callback => {
  Console.WriteLine("Tracking identifier: " + callback);
});
```

**Android Syntax**

```csharp
public unsafe static void GetTrackingIdentifier (IAdobeCallback callback);
```

* _callback_ is a callback containing the tracking Identifier string value.

**Android Example**

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

## getTrackingIdentifierWithCompletionHandler <a id="getTrackingIdentifierWithCompletionHandler"></a>

{% hint style="warning" %}
Before you use this API, see [Identify unique visitors](https://docs.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-overview.html).
{% endhint %}

Retrieves the Analytics tracking identifier that is generated for this app/device instance. This identifier is an app-specific, unique visitor ID that is generated at the initial launch and is stored and used after the initial launch. The ID is preserved between app upgrades and is removed when the app is uninstalled. Invoke the callback with NSError if unexpected error occures or request times out.

{% hint style="info" %}
If you have an [Experience Cloud ID](https://app.gitbook.com/@aep-sdks/s/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#get-experience-cloud-ids), and have not yet configured a visitor ID grace period, the value returned by `getTrackingIdentifier` might be null.
{% endhint %}

{% tabs %}
{% tab title="iOS (ACP 2.x)" %}

### getTrackingIdentifierWithCompletionHandler

#### Syntax

```objectivec
+ (void) getTrackingIdentifierWithCompletionHandler: (nonnull void (^) (NSString* __nullable trackingIdentifier, NSError* __nullable error)) completionHandler;
```

* _completionHandler_ is invoked with the tracking Identifier string value. or an NSError if an unexpected error occurs or the request times out.

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPAnalytics getTrackingIdentifierWithCompletionHandler:^(NSString * _Nullable trackingIdentifier, NSError * _Nullable error) {
    // use queue size or handle error
}];
```

**Swift**

```swift
ACPAnalytics.getTrackingIdentifierWithCompletionHandler { (trackingIdentifier, error) in    
     // use queue size or handle error  
}
```
{% endtab %}
{% endtabs %}

## getVisitorIdentifier <a id="getvisitoridentifier"></a>

{% hint style="warning" %}
Before using this API, see [Identify unique visitors](https://docs.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-overview.html).
{% endhint %}

This API gets a custom Analytics visitor identifier, which has been set previously using [setVisitorIdentifier](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#setidentifier).

{% tabs %}
{% tab title="Android" %}
### getVisitorIdentifier

#### Syntax

```java
public static void getVisitorIdentifier(AdobeCallback<String> callback)
```

* _callback_ is invoked with the visitor identifier value. When an AdobeCallbackWithError is provided, an AdobeError can be returned in the eventuality of an unexpected error or if the default timeout \(5000ms\) is met before the callback is returned with visitor identifier.

#### Example

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

### getVisitorIdentifier

#### Syntax

```swift
static func getVisitorIdentifier(completion: @escaping (String?, Error?) -> Void)
```

* _callback_ is invoked with the visitor identifier value.

#### Example

**Swift**

```swift
Analytics.getVisitorIdentifier { (visitorId, _) in
   // check the visitorIdentifier value or handle error
}
```

**Objective-C**

```objectivec
[AEPMobileAnalytics getVisitorIdentifier:^(NSString * _Nullable visitorIdentifier, NSError * _Nullable error) {
    // check the visitorIdentifier value or handle error
}];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### getVisitorIdentifier

#### Syntax

```objectivec
+ (void) getVisitorIdentifier: (nonnull void (^) (NSString* __nullable visitorIdentifier)) callback;
```

* _callback_ is invoked with the visitor identifier value.

#### Example

**Objective-C**

```objectivec
[ACPAnalytics getVisitorIdentifier:^(NSString * _Nullable visitorIdentifier) {
    // check the visitorIdentifier value   
}];
```

**Swift**

```swift
ACPAnalytics.getVisitorIdentifier { (visitorIdentifier) in
    // check the visitorIdentifier value  
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### getVisitorIdentifier

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
#### Dart

### getVisitorIdentifier

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
#### Cordova

### getVisitorIdentifier

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
#### C\#

### GetVisitorIdentifier

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
#### C\#

### GetVisitorIdentifier

**iOS Syntax**

```csharp
public unsafe static void GetVisitorIdentifier (Action<NSString> callback);
```

* _callback_ is a callback containing the visitor Identifier string value.

**iOS Example**

```csharp
ACPAnalytics.GetVisitorIdentifier(callback => {
  Console.WriteLine("Visitor identifier: " + callback);
});
```

**Android Syntax**

```csharp
public unsafe static void GetVisitorIdentifier (IAdobeCallback callback);
```

* _callback_ is a callback containing the visitor Identifier string value.

**Android Example**

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

## getVisitorIdentifierWithCompletionHandler <a id="getVisitorIdentifierWithCompletionHandler"></a>

{% hint style="warning" %}
Before using this API, see [Identify unique visitors](https://docs.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-overview.html).
{% endhint %}

This API gets a custom Analytics visitor identifier, which has been set previously using [setVisitorIdentifier](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#setidentifier). Callback with NSError if an unexpected error occurs or the request times out.

{% tabs %}
{% tab title="iOS (ACP 2.x)" %}

### getVisitorIdentifier

#### Syntax

```objectivec
+ (void) getVisitorIdentifierWithCompletionHandler: (nonnull void (^) (NSString* __nullable visitorIdentifier, NSError* __nullable error)) completionHandler;
```

* _completionHandler_ is invoked with the visitor identifier value or an NSError if an unexpected error occurs or the request times out.

#### Example

**Objective-C**

```objectivec
[ACPAnalytics getVisitorIdentifierWithCompletionHandler:^(NSString * _Nullable visitorIdentifier, NSError * _Nullable error) {
    // check the visitorIdentifier value or handle error
}];
```

**Swift**

```swift
ACPAnalytics.getVisitorIdentifierWithCompletionHandler { (visitorIdentifier, error) in
    // check the visitorIdentifier value or handle error
}
```
{% endtab %}
{% endtabs %}

## sendQueuedHits <a id="sendqueuedhits"></a>

Sends all queued hits to Analytics, regardless of the current hit batch settings.

{% tabs %}
{% tab title="Android" %}
### sendQueuedHits

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

#### **Syntax**

```java
public static void sendQueuedHits()
```

#### **Example**

```java
Analytics.sendQueuedHits();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### sendQueuedHits

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

#### Syntax

```swift
static func sendQueuedHits()
```

#### Example

**Objective-C**

```objectivec
Analytics.sendQueuedHits()
```

**Swift**

```swift
[AEPMobileAnalytics sendQueueHits];
```

{% tab title="iOS (ACP 2.x)" %}

### sendQueuedHits

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

{% hint style="warning" %}
Use caution when manually clearing the queue. This process cannot be reversed.
{% endhint %}

#### Syntax

```objectivec
+ (void) sendQueuedHits;
```

#### Example

**Objective-C**

```objectivec
[ACPAnalytics sendQueuedHits];
```

**Swift**

```swift
ACPAnalytics.sendQueuedHits()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### sendQueuedHits

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

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
#### Dart

### sendQueuedHits

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
#### Cordova

### sendQueuedHits

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
#### C\#

### SendQueuedHits

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
#### C\#

### SendQueuedHits

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

## setVisitorIdentifier <a id="setidentifier"></a>

{% hint style="warning" %}
Before using this API, see [Identify unique visitors](https://docs.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-overview.html).
{% endhint %}

Sets a custom Analytics visitor identifier. For more information, see [Custom Visitor ID](https://marketing.adobe.com/resources/help/en_US/sc/implement/visid_custom.html).

{% tabs %}
{% tab title="Android" %}
### setVisitorIdentifier

#### Syntax

```java
 public static void setVisitorIdentifier(final String visitorIdentifier)
```

* _visitorIdentifier_ is the new value for the visitor identifier.

#### Example

```java
Analytics.setVisitorIdentifier("custom_identifier");
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### setVisitorIdentifier

#### Syntax

```swift
static func setVisitorIdentifier(visitorIdentifier: String)
```

* _visitorIdentifier_ is the new value for the visitor identifier.

#### Example

**Swift**

```swift
Analytics.setVisitorIdentifier(visitorIdentifier:"custom_identifier")
```

**Objective-C**

```objectivec
[AEPMobileAnalytics setVisitorIdentifier:@"custom_identifier"];
```



{% tab title="iOS (ACP 2.x)" %}
### setVisitorIdentifier

#### Syntax

```objectivec
+ (void) setVisitorIdentifier: (nonnull NSString*) visitorIdentifier;
```

* _visitorIdentifier_ is the new value for the visitor identifier.

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPAnalytics setVisitorIdentifier:@"custom_identifier"];
```

**Swift**

```swift
ACPAnalytics.setVisitorIdentifier("custom_identifier")
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### setVisitorIdentifier

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
#### Dart

### setVisitorIdentifier

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
#### Cordova

### setVisitorIdentifier

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
#### C\#

### SetVisitorIdentifier

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
#### C\#

### SetVisitorIdentifier

**iOS Syntax**

```text
public static void SetVisitorIdentifier (string visitorIdentifier);
```

* _visitorIdentifier_ is the new value for the visitor identifier.

**Android Syntax**

```text
public unsafe static void SetVisitorIdentifier (string visitorID);
```

* _visitorID_ is the new value for the visitor identifier.

**Example**

```text
ACPAnalytics.SetVisitorIdentifier("VisitorIdentifier");
```
{% endtab %}
{% endtabs %}

