# Media API Reference

## Create Media Tracker Instance<a id="createtracker"></a>

Creates an instance of media tracker to track playback session.

{% tabs %}
{% tab title="Android" %}
### createTracker

#### Syntax

```java
public static void createTracker(AdobeCallback<MediaTracker> callback)
```

#### **Example**

```java
AdobeCallback<String> mediaTrackerCallback = new AdobeCallback<String>() {
    @Override
    public void call(final MediaTracker mediaTracker) {
        // Use the media tracker instance for tracking.
    }
};
Media.createTracker(mediaTrackerCallback);
```
{% endtab %}

{% tab title="iOS" %}
### createTracker

#### Syntax

```objectivec
+(void) createTracker: (void (^ _Nonnull) (ACPMediaTracker* _Nullable)) callback;

```

#### Example

Here are examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the media tracker instance for tracking.
}
```

**Swift**

```swift
ACPMedia.createTracker({mediaTracker in
    // Use the media tracker instance for tracking.
}
```
{% endtab %}
{% endtabs %}