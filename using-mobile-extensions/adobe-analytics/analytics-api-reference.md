# Analytics API reference

## Send queued hits <a id="sendqueuedhits"></a>

Sends all queued hits to Analytics, regardless of the current hit batch settings.

{% tabs %}
{% tab title="Android" %}
### sendQueuedHits

Regardless of how many hits are currently queued, this method forces the library to send all hits in the offline queue.

**Warning:** Use caution when manually clearing the queue. This process cannot be reversed.

#### **Syntax**

```java
public static void sendQueuedHits()
```

#### **Example**

```java
Analytics.sendQueuedHits();
```
{% endtab %}

{% tab title="iOS" %}
### sendQueuedHits

Regardless of how many hits are currently queued, this method forces the library to send all hits in the offline queue.

**Warning:** Use caution when manually clearing the queue. This process cannot be reversed.

#### Syntax

```objectivec
+ (void) sendQueuedHits;
```

#### Example

Here are examples in Objective-C and Swift:

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

Regardless of how many hits are currently queued, this method forces the library to send all hits in the offline queue.

```jsx
ACPAnalytics.sendQueuedHits();
```
{% endtab %}
{% endtabs %}

## Clear queued hits <a id="clearqueue"></a>

Force delete, without sending to Analytics, all hits being stored or batched on the SDK.

{% tabs %}
{% tab title="Android" %}
### clearQueue

**Warning:** Use caution when manually clearing the queue. This process cannot be reversed.

#### Syntax

```java
public static void clearQueue()
```

#### Example

```java
Analytics.clearQueue();
```
{% endtab %}

{% tab title="iOS" %}
### clearQueue

**Warning:** Use caution when manually clearing the queue. This process cannot be reversed.

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

**Warning:** Use caution when manually clearing the queue. This process cannot be reversed.

```jsx
ACPAnalytics.clearQueue();
```
{% endtab %}
{% endtabs %}

## Get the queue size <a id="getqueuesize"></a>

Retrieves the total number of Analytics hits in the tracking queue.

{% tabs %}
{% tab title="Android" %}
### getQueueSize

#### Syntax

```java
 public static void getQueueSize(final AdobeCallback<Long> callback)
```

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

{% tab title="iOS" %}
### getQueueSize

#### Syntax

```objectivec
+ (void) getQueueSize: (nonnull void (^) (NSUInteger queueSize)) callback;
```

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

```jsx
ACPAnalytics.getQueueSize().then(size => console.log("AdobeExperienceSDK: Queue size: " + size));
```
{% endtab %}
{% endtabs %}

## Get the tracking identifier <a id="gettrackingidentifier"></a>

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

#### **Example**

```java
AdobeCallback<String> trackingIdentifierCallback = new AdobeCallback<String>() {
    @Override
    public void call(final String trackingIdentifier) {
        // check the trackingIdentifier value    
    }
};
Analytics.getTrackingIdentifier(analyticsTrackingIdentifierCallback);
```
{% endtab %}

{% tab title="iOS" %}
### getTrackingIdentifier

Retrieves the Analytics tracking identifier.

#### Syntax

```objectivec
+ (void) getTrackingIdentifier: (nonnull void (^) (NSString* __nullable trackingIdentifier)) callback;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPAnalytics getTrackingIdentifier:^(NSString * _Nullable trackingIdentifier) {
    // use returned trackingIdentifier   
}];
```

**Swift**

```swift
ACPAnalytics.getTrackingIdentifier { (trackingIdentifier) in
    // use returned trackingIdentifier
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### getTrackingIdentifier

Retrieves the Analytics tracking identifier.

```jsx
ACPAnalytics.getTrackingIdentifier().then(identifier => console.log("AdobeExperienceSDK: Tracking identifier: " + identifier));
```
{% endtab %}
{% endtabs %}

## Set the custom visitor identifier <a id="setidentifier"></a>

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

#### Example

```java
Analytics.setVisitorIdentifier("custom_identifier");
```
{% endtab %}

{% tab title="iOS" %}
### setVisitorIdentifier

#### Syntax

```objectivec
+ (void) setVisitorIdentifier: (nonnull NSString*) visitorIdentifier;
```

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

```jsx
ACPAnalytics.setVisitorIdentifier("yourVisitorId");
```
{% endtab %}
{% endtabs %}

## Get the custom visitor identifier <a id="getvisitoridentifier"></a>

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

#### Example

```java
AdobeCallback<String> visitorIdentifierCallback = new AdobeCallback<String>() {
    @Override
    public void call(final String visitorIdentifier) {
        // check the visitorIdentifier value    
    }
};

Analytics.getVisitorIdentifier(visitorIdentifierCallback);
```
{% endtab %}

{% tab title="iOS" %}
### getVisitorIdentifier

#### Syntax

```objectivec
+ (void) getVisitorIdentifier: (nonnull void (^) (NSString* __nullable visitorIdentifier)) callback;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPAnalytics getVisitorIdentifier:^(NSString * _Nullable visitorIdentifier) {
    // use returned visitorIdentifier   
}];
```

**Swift**

```swift
ACPAnalytics.getVisitorIdentifier { (visitorIdentifier) in
    // use returned visitorIdentifier
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### getVisitorIdentifier

```jsx
ACPAnalytics.getVisitorIdentifier().then(vid => console.log("AdobeExperienceSDK: Visitor identifier: " + vid));
```
{% endtab %}
{% endtabs %}

