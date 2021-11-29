# Analytics API reference

## clearQueue <a id="clearqueue"></a>

Force delete, without sending to Analytics, all hits being stored or batched on the SDK.

{% tabs %}
{% tab title="Android" %}
### clearQueue

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

**Syntax**

```java
public static void clearQueue()
```

**Example**

```java
Analytics.clearQueue();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
### clearQueue

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

**Syntax**

```swift
static func clearQueue()
```

**Example**

**Swift**

```swift
Analytics.clearQueue()
```

**Objective-C**

```text
[AEPMobileAnalytics clearQueue];
```
{% endtab %}
{% endtabs %}

## extensionVersion <a id="extensionversion"></a>

The `extensionVersion()` API returns the version of the Analytics extension that is registered with the Mobile Core extension.

To get the version of the Analytics extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
**Java**

```java
String analyticsExtensionVersion = Analytics.extensionVersion();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Swift**

```swift
let version = Analytics.extensionVersion
```

**Objective-C**

```text
NSString *version = [AEPMobileAnalytics extensionVersion];
```
{% endtab %}
{% endtabs %}

## getQueueSize <a id="getqueuesize"></a>

Retrieves the total number of Analytics hits in the tracking queue.

{% tabs %}
{% tab title="Android" %}
### getQueueSize

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

{% tab title="iOS \(AEP 3.x\)" %}
### getQueueSize

Please use the [getQueueSizeWithCompletionHandler](analytics-api-reference.md#getqueuesizewithcompletionhandler) API instead.
{% endtab %}
{% endtabs %}

## getQueueSizeWithCompletionHandler <a id="getqueuesizewithcompletionhandler"></a>

Retrieves the total number of Analytics hits in the tracking queue. Invoke the callback with NSError if an unexpected error occurs or the request times out.

{% tabs %}
{% tab title="iOS \(AEP 3.x\)" %}
### getQueueSize

**Syntax**

```swift
static func getQueueSize(completion: @escaping (Int, Error?) -> Void)
```

**Example**

The following examples are shown in both Swift and Objective-C.

**Swift**

```swift
Analytics.getQueueSize { (queueSize, error) in
    // Handle error (if non-nil) or use queueSize.
}
```

**Objective-C**

```text
[AEPMobileAnalytics getQueueSize:^(NSInteger queueSize, NSError * _Nullable error) {
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
### getTrackingIdentifier

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

{% tab title="iOS \(AEP 3.x\)" %}
### getTrackingIdentifier

Retrieves the Analytics tracking identifier. See [getTrackingIdentifierWithCompletionHandler](analytics-api-reference.md#gettrackingidentifierwithcompletionhandler)
{% endtab %}
{% endtabs %}

## getTrackingIdentifierWithCompletionHandler <a id="gettrackingidentifierwithcompletionhandler"></a>

{% hint style="warning" %}
Before you use this API, please read the documentation on [identifying unique visitors](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html).
{% endhint %}

Retrieves the Analytics tracking identifier that is generated for this app/device instance. This identifier is an app-specific, unique visitor ID that is generated at the initial launch and is stored and used after the initial launch. The ID is preserved between app upgrades and is removed when the app is uninstalled. Invoke the callback with NSError if an unexpected error occurs or the request times out.

{% hint style="info" %}
If you have an [Experience Cloud ID](https://app.gitbook.com/@aep-sdks/s/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#getexperiencecloudid) and have not yet configured a visitor ID grace period, the value returned by `getTrackingIdentifier` might be null.
{% endhint %}

{% tabs %}
{% tab title="iOS \(AEP 3.x\)" %}
### getTrackingIdentifier

Retrieves the Analytics tracking identifier.

**Syntax**

```swift
static func getTrackingIdentifier(completion: @escaping (String?, Error?) -> Void)
```

**Example**

**Swift**

```swift
Analytics.getTrackingIdentifier { (trackingId, error) in
   // Handle the error (if non-nil) or use the trackingIdentifier value
}
```

**Objective-C**

```text
AEPMobileAnalytics getTrackingIdentifier:^(NSString * _Nullable trackingIdentifier, NSError * _Nullable error) {
   // Handle the error (if non-nil) or use the trackingIdentifier value
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
### getVisitorIdentifier

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

{% tab title="iOS \(AEP 3.x\)" %}
### getVisitorIdentifier

See [getVisitorIdentifierWithCompletionHandler](analytics-api-reference.md#getvisitoridentifierwithcompletionHandler)
{% endtab %}
{% endtabs %}

## getVisitorIdentifierWithCompletionHandler <a id="getvisitoridentifierwithcompletionhandler"></a>

{% hint style="warning" %}
Before using this API, see [Identify unique visitors](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html).
{% endhint %}

This API gets a custom Analytics visitor identifier, which has been set previously using [setVisitorIdentifier](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-api-reference#setvisitoridentifier). Callback with NSError if an unexpected error occurs or the request times out.

{% tabs %}
{% tab title="iOS \(AEP 3.x\)" %}
### getVisitorIdentifier

**Syntax**

```swift
static func getVisitorIdentifier(completion: @escaping (String?, Error?) -> Void)
```

**Example**

**Swift**

```swift
Analytics.getVisitorIdentifier { (visitorIdentifier, error) in
   // Handle the error (if non-nil) or use the visitorIdentifier value
}
```

**Objective-C**

```text
[AEPMobileAnalytics getVisitorIdentifier:^(NSString * _Nullable visitorIdentifier, NSError * _Nullable error) {
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
### sendQueuedHits

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

**Syntax**

```java
public static void sendQueuedHits()
```

**Example**

```java
Analytics.sendQueuedHits();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
### sendQueuedHits

This method forces the library to send all hits in the offline queue, regardless of how many hits are currently queued.

{% hint style="warning" %}
Use caution when manually clearing the queue. This operation cannot be reverted.
{% endhint %}

**Syntax**

```swift
static func sendQueuedHits()
```

**Example**

**Objective-C**

```text
Analytics.sendQueuedHits()
```

**Swift**

```swift
[AEPMobileAnalytics sendQueueHits];
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
### setVisitorIdentifier

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

{% tab title="iOS \(AEP 3.x\)" %}
### setVisitorIdentifier

**Syntax**

```swift
static func setVisitorIdentifier(visitorIdentifier: String)
```

* _visitorIdentifier_ is the new value for the visitor identifier.

**Example**

**Swift**

```swift
Analytics.setVisitorIdentifier(visitorIdentifier:"custom_identifier")
```

**Objective-C**

```text
[AEPMobileAnalytics setVisitorIdentifier:@"custom_identifier"];
```
{% endtab %}
{% endtabs %}
