# Analytics API Reference

## Get tracking identifier {#gettrackingidentifier}

Retrieves the Analytics tracking identifier generated for this app/device instance. This identifier is an app-specific, unique visitor ID that is generated at the initial launch and is stored and used after the initial launch.The ID is preserved between app upgrades and is removed when the app is uninstalled.  


{% tabs %}
{% tab title="Android" %}
#### Java

### getTrackingIdentifier

#### Syntax

```java
public static void  getTrackingIdentifier(final AdobeCallback<String> callback);
```

#### Example

```java
Analytics.getTrackingIdentifier(new AdobeCallback<String>() {    
    @Override    
    public void call(final String trackingIdentifier) {        
        // check the trackingIdentifier value    
    }
});
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

### getTrackingIdentifier

#### Syntax

```objective-c
+ (void) getTrackingIdentifier: (nonnull void (^) (NSString* __nullable trackingIdentifier)) callback;
```

#### Example

```objective-c
[ACPAnalytics getTrackingIdentifier:^(NSString * _Nullable trackingIdentifier) {
    // check trackingIdentifier parameter for the value
}];
```

{% endtab %}
{% endtabs %}

## Send queued hits {#sendqueuedhits}

Sends all queued hits to Analytics, regardless of the current hit batch settings.

{% tabs %}
{% tab title="Android" %}
#### Java

### sendQueuedHits

#### **Syntax**

```java
public static void sendQueuedHits();
```

#### **Example**

```java
Analytics.sendQueuedHits();
```
{% endtab %}

{% tab title="iOS" %}

#### Objective-C

### sendQueuedHits

#### Syntax

```objective-c
+ (void) sendQueuedHits;
```

#### Example

```objective-c
[ACPAnalytics sendQueuedHits];
```

{% endtab %}
{% endtabs %}

## Get queue size {#sendqueuedhits}

Retrieves the total number of Analytics hits In the tracking queue.

{% tabs %}
{% tab title="Android" %}
#### Java

### getQueueSize

#### Syntax

```java
public static void getQueueSize(final AdobeCallback<Long> callback);
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

#### Objective-C

### getQueueSize

#### Syntax

```objective-c
+ (void) getQueueSize: (nonnull void (^) (NSUInteger queueSize)) callback;
```

#### Example

```objective-c
[ACPAnalytics getQueueSize:^(NSUInteger queueSize) {
    // check queueSize parameter for value
}];
```

{% endtab %}
{% endtabs %}

