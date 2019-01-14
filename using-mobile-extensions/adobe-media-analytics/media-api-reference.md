# Media API Reference

## Create Media Tracker Instance

Use this API to create an instance of media tracker to track playback session.

{% tabs %}
{% tab title="Android" %}
### createTracker

The callback will be invoked to return the created tracker instance, or in case of error, `null` is returned.

#### Syntax

```java
public static void createTracker(AdobeCallback<MediaTracker> callback)
```

#### Example

```java
Media.createTracker(new AdobeCallback<String>() {
    @Override
    public void call(final MediaTracker mediaTracker) {
        // Use the media tracker instance for tracking.
    }
});
```

{% endtab %}

{% tab title="iOS" %}
### createTracker

The callback will be invoked to return the created tracker instance, or in case of error, `nil` is returned.

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
}];
```

**Swift**

```swift
ACPMedia.createTracker({mediaTracker in
    // Use the media tracker instance for tracking.
}
```
{% endtab %}
{% endtabs %}

## Create Media Object

Use this API to create a Dictionary instance which represents the MediaObject.

{% tabs %}
{% tab title="Android" %}
### createMediaObject

#### Syntax

```java
<<<<TODO API >>>>
```

#### Example

```java

<<<<TODO EXAMPLE >>>>
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
}];
```

**Swift**

```swift
ACPMedia.createTracker({mediaTracker in
    // Use the media tracker instance for tracking.
}
```
{% endtab %}
{% endtabs %}

