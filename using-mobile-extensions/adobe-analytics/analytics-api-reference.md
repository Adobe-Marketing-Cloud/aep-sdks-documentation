# Analytics API Reference

## Get tracking identifier {#gettrackingidentifier}

Retrieves the Analytics tracking identifier generated for this app/device instance. This identifier is an app-specific, unique visitor ID that is generated at the initial launch and is stored and used after the initial launch.The ID is preserved between app upgrades and is removed when the app is uninstalled.  


{% tabs %}
{% tab title="Android" %}
#### Java

### getTrackingIdentifier

#### Syntax

```text
 public static void  getTrackingIdentifier(final AdobeCallback<String> callback)
```

#### **Example**

```text
AdobeCallback<String> trackingIdentifierCallback = new AdobeCallback<String>() {    @Override    public void call(final String trackingIdentifier) {        // check the trackingIdentifier value    }};Analytics.getTrackingIdentifier(analyticsTrackingIdentifierCallback);
```
{% endtab %}

{% tab title="iOS" %}

{% endtab %}
{% endtabs %}

## Send queued hits {#sendqueuedhits}

Sends all queued hits to Analytics, regardless of the current hit batch settings.

{% tabs %}
{% tab title="Android" %}
#### Java

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

{% endtab %}
{% endtabs %}

