# Edge API reference

## extensionVersion <a id="extensionversion"></a>

Returns the version of the client-side Edge extension.

{% tabs %}
{% tab title="Android" %}

#### Java

##### Syntax

```java
public static String extensionVersion();
```

##### Example

```java
Edge.extensionVersion();
```

{% endtab %}

{% tab title="iOS" %}

#### Swift

##### Syntax

```swift
public static let extensionVersion
```

##### Example

```swift
Edge.extensionVersion
```

#### Objective-C

##### Syntax

```objective-c
// Swift Edge
public static let extensionVersion
```

##### Example

```objective-c
[AEPMobileEdge extensionVersion];
```

{% endtab %}

{% endtabs %}

## sendEvent <a id="sendevent"></a>

Sends an Experience event to Adobe Experience Edge Network.

{% tabs %}
{% tab title="Android" %}

#### Java

##### Syntax

```java
public static void sendEvent(final ExperienceEvent experienceEvent, final EdgeCallback callback);
```

- *experienceEvent* - the XDM Experience Event to be sent to Adobe Experience Edge Network
- *callback* - optional callback to be invoked when the request is complete, returning the associated response handles received from the Adobe Experience Edge Network. It may be invoked on a different thread.

##### Example

```java
// example 1 - send the experience event without handling the Edge Network response
Edge.sendEvent(experienceEvent, null);

// example 2 - send the experience event and handle the Edge Network response onComplete
Edge.sendEvent(experienceEvent, new EdgeCallback() {
  @Override
  public void onComplete(final List<EdgeEventHandle> handles) {
		// handle the Edge Network response 
  }
});
```

{% endtab %}

{% tab title="iOS" %}

#### Swift

##### Syntax

```swift
static func sendEvent(experienceEvent: ExperienceEvent, _ completion: (([EdgeEventHandle]) -> Void)? = nil)
```

- *experienceEvent* - the XDM Experience Event to be sent to Adobe Experience Edge Network
- *completion* - optional completion handler to be invoked when the request is complete, returning the associated response handles received from the Adobe Experience Edge Network. It may be invoked on a different thread.

##### Example

```swift
// example 1 - send the experience event without handling the Edge Network response
Edge.sendEvent(experienceEvent: experienceEvent)

// example 2 - send the experience event and handle the Edge Network response onComplete
Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
            // handle the Edge Network response
        }
```

#### Objective-C

##### Syntax

```objective-c
// Swift Edge
static func sendEvent(experienceEvent: ExperienceEvent, _ completion: (([EdgeEventHandle]) -> Void)? = nil)
```

##### Example

```objective-c
// example 1 - send the experience event without handling the Edge Network response
[AEPMobileEdge sendExperienceEvent:event completion:nil];

// example 2 - send the experience event and handle the Edge Network response onComplete
[AEPMobileEdge sendExperienceEvent:event completion:^(NSArray<AEPEdgeEventHandle *> * _Nonnull handles) {
  // handle the Edge Network response
}];
```

{% endtab %}

{% endtabs %}

## registerExtension <a id="registerextension"></a>

Registers the Edge extension with the Mobile Core SDK.

{% tabs %}
{% tab title="Android" %}

#### Java

##### Syntax

```java
public static void registerExtension();
```

##### Example

```java
Edge.registerExtension();
```

{% endtab %}

{% tab title="iOS" %}

#### Swift

Use the MobileCore API to register the Edge extension.

##### Syntax

```swift
// MobileCore
public static func registerExtensions(_ extensions: [Extension.Type], _ completion: (() -> Void)? = nil)
```

##### Example

```swift
MobileCore.registerExtensions([Edge.self, ...], {
  // processing after registration
})
```

#### Objective-C

Use the AEPMobileCore API to register the Edge extension.

##### Syntax

```objective-c
// Swift MobileCore
public static func registerExtensions(_ extensions: [Extension.Type], _ completion: (() -> Void)? = nil)
```

##### Example

```objective-c
[AEPMobileCore registerExtensions:@[AEPMobileEdge.class, ...] completion:^{
  // processing after registration
}];
```

{% endtab %}

{% endtabs %}