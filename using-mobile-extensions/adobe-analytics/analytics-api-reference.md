# Analytics API reference

## Send queued hits     <a id="sendqueuedhits"></a>

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
{% endtabs %}

## Clear queued hits  <a id="sendqueuedhits"></a>

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
{% endtabs %}

## Get the queue size     <a id="sendqueuedhits"></a>

Retrieves the total number of Analytics hits In the tracking queue.

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
{% endtabs %}

## Get the tracking identifier     <a id="gettrackingidentifier"></a>

{% hint style="warning" %}
Please review Adobe Analytics's [Visitor ID Order documentation](https://marketing.adobe.com/resources/help/en_US/sc/implement/visid_overview.html) before using this API.
{% endhint %}

Retrieves the Analytics tracking identifier that is generated for this app/device instance. This identifier is an app-specific, unique visitor ID that is generated at the initial launch and is stored and used after the initial launch. The ID is preserved between app upgrades and is removed when the app is uninstalled.

{% hint style="info" %}
If you have an [Experience Cloud ID](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/267ffce7f3550c0b85a54b8d4603ae3fe74d5a15/using-mobile-extensions/mobile-core/identity/identity-api-reference/README.md#get-experience-cloud-ids), and do not have visitor ID grace period configured, the value returned by `getTrackingIdentifier` might be null.
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
{% endtabs %}

## Set the custom visitor identifier    <a id="setidentifier"></a>

{% hint style="warning" %}
Please review Adobe Analytics's [Visitor ID Order documentation](https://marketing.adobe.com/resources/help/en_US/sc/implement/visid_overview.html) before using this API.
{% endhint %}

Sets a custom Analytics visitor identifier. Please see [Custom Visitor ID](https://marketing.adobe.com/resources/help/en_US/sc/implement/visid_custom.html) for more information.

{% tabs %}
{% tab title="Android" %}
### setVistorIdentifier

#### Syntax

```java
 public static void setVistorIdentifier(final String visitorIdentifier)
```

#### Example

```java
Analytics.setVistorIdentifier("custom_identifier");
```
{% endtab %}

{% tab title="iOS" %}
### setVistorIdentifier

#### Syntax

```objectivec
+ (void) setVistorIdentifier: (nonnull NSString*) visitorIdentifier;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPAnalytics setVistorIdentifier:@"custom_identifier"];
```

**Swift**

```swift
ACPAnalytics.setVistorIdentifier("custom_identifier")
```
{% endtab %}
{% endtabs %}

## Get the custom visitor identifier

{% hint style="warning" %}
Please review Adobe Analytics's [Visitor ID Order documentation](https://marketing.adobe.com/resources/help/en_US/sc/implement/visid_overview.html) before using this API.
{% endhint %}

Sets a custom Analytics visitor identifier. Please see [Custom Visitor ID](https://marketing.adobe.com/resources/help/en_US/sc/implement/visid_custom.html) for more information.

{% tabs %}
{% tab title="Android" %}
### getVistorIdentifier

#### Syntax

```java
public static void getVisitorIdentifier(AdobeCallback<String> callback)
```
{% endtab %}

{% tab title="iOS" %}
### getVistorIdentifier

#### Syntax

```objectivec
+ (void) getVisitorIdentifier: (nonnull void (^) (NSString* __nullable visitorIdentifier)) callback;
```

\*\*\*\*
{% endtab %}
{% endtabs %}

