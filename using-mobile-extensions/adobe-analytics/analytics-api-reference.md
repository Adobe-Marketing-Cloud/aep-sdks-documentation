# Analytics API reference

## Get the Tracking Identifier <a id="gettrackingidentifier"></a>

Retrieves the Analytics tracking identifier generated for this app/device instance. This identifier is an app-specific, unique visitor ID that is generated at the initial launch and is stored and used after the initial launch.The ID is preserved between app upgrades and is removed when the app is uninstalled.  


{% tabs %}
{% tab title="Android" %}
### getTrackingIdentifier

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

Retrieves the analytics tracking identifier.

#### Syntax

```objectivec
+ (void) getTrackingIdentifier: (nonnull void (^) (NSString* __nullable trackingIdentifier)) callback;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPAnalytics getTrackingIdentifier:^(NSString * _Nullable trackingIdentifier) {
    // use returned tracking id    
    NSLog(@"Tracking ID : %@", trackingIdentifier);}];
```

**Swift**

```swift
ACPAnalytics.getTrackingIdentifier { (trackingIdentifier) in
            //use returned tracking id
            print(trackingIdentifier!)
        }
```
{% endtab %}
{% endtabs %}

## Send Queued Hits <a id="sendqueuedhits"></a>

Sends all queued hits to Analytics, regardless of the current hit batch settings.

{% tabs %}
{% tab title="Android" %}
### sendQueuedHits

#### **Syntax**

```text
public static void sendQueuedHits()
```

#### **Example**

```text
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

## Get the Queue Size <a id="sendqueuedhits"></a>

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

Forces the library to send all queued hits regardless of the current batch options.

#### Syntax

Here are examples in Objective-C and Swift:

```objectivec
+ (void) getQueueSize: (nonnull void (^) (NSUInteger queueSize)) callback;
```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPAnalytics getQueueSize: ^(NSUInteger queueSize) {    // use queue size}];
```

**Swift**

```swift
ACPAnalytics.getQueueSize({queueSize in    
     // use queue size   
})
```
{% endtab %}
{% endtabs %}

