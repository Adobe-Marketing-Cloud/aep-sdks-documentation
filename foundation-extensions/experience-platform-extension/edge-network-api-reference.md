# Edge Network API reference

## extensionVersion <a id="extensionversion"></a>

Returns the version of the client-side Edge extension.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static String extensionVersion();
```

#### Example

```java
Edge.extensionVersion();
```
{% endtab %}

{% tab title="iOS" %}
### Swift

#### Syntax

```swift
public static let extensionVersion
```

#### Example

```swift
Edge.extensionVersion
```

### Objective-C

#### Syntax

```text
// Swift Edge
public static let extensionVersion
```

#### Example

```text
[AEPMobileEdge extensionVersion];
```
{% endtab %}
{% endtabs %}

## sendEvent <a id="sendevent"></a>

Sends an Experience event to Adobe Experience Edge Network.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void sendEvent(final ExperienceEvent experienceEvent, final EdgeCallback callback);
```

* _experienceEvent_ - the XDM Experience Event to be sent to Adobe Experience Edge Network
* _callback_ - optional callback to be invoked when the request is complete, returning the associated response handles received from the Adobe Experience Edge Network. It may be invoked on a different thread.

#### Example

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
### Swift

#### Syntax

```swift
static func sendEvent(experienceEvent: ExperienceEvent, _ completion: (([EdgeEventHandle]) -> Void)? = nil)
```

* _experienceEvent_ - the XDM Experience Event to be sent to Adobe Experience Edge Network
* _completion_ - optional completion handler to be invoked when the request is complete, returning the associated response handles received from the Adobe Experience Edge Network. It may be invoked on a different thread.

#### Example

```swift
// example 1 - send the experience event without handling the Edge Network response
Edge.sendEvent(experienceEvent: experienceEvent)

// example 2 - send the experience event and handle the Edge Network response onComplete
Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
            // handle the Edge Network response
        }
```

### Objective-C

#### Syntax

```text
// Swift Edge
static func sendEvent(experienceEvent: ExperienceEvent, _ completion: (([EdgeEventHandle]) -> Void)? = nil)
```

#### Example

```text
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
### Java

#### Syntax

```java
public static void registerExtension();
```

#### Example

```java
Edge.registerExtension();
```
{% endtab %}

{% tab title="iOS" %}
### Swift

Use the MobileCore API to register the Edge extension.

#### Syntax

```swift
// MobileCore
public static func registerExtensions(_ extensions: [Extension.Type], _ completion: (() -> Void)? = nil)
```

#### Example

```swift
MobileCore.registerExtensions([Edge.self, ...], {
  // processing after registration
})
```

### Objective-C

Use the AEPMobileCore API to register the Edge extension.

#### Syntax

```text
// Swift MobileCore
public static func registerExtensions(_ extensions: [Extension.Type], _ completion: (() -> Void)? = nil)
```

#### Example

```text
[AEPMobileCore registerExtensions:@[AEPMobileEdge.class, ...] completion:^{
  // processing after registration
}];
```
{% endtab %}
{% endtabs %}

## Public classes

{% tabs %}
{% tab title="Android" %}
### Java

#### Schema and Property interfaces

The Edge extension provides the following interfaces:

* Schema
* Property

By using the Edge extension, the **Schema** interface can be used to define the classes that are associated with your defined schema in Adobe Experience Platform.

```java
/**
 * The interface that represents an Experience XDM event data schema.
 */
public interface Schema {

    /**
     * Returns the version of this schema as defined in the Adobe Experience Platform.
     * @return the version of this schema.
     */
    String getSchemaVersion();

    /**
     * Returns the identifier for this schema as defined in the Adobe Experience Platform.
     * The identifier is a URI where this schema is defined.
     * @return the URI identifier for this schema.
     */
    String getSchemaIdentifier();

    /**
     * Returns the identifier for this dataset as defined in the Adobe Experience Platform.
     * @return the dataset ID
     */
    String getDatasetIdentifier();

    /**
     * Serialize this {@code Schema} object to a map with the same format as its XDM schema.
     * @return the XDM-formatted map of this {@code Schema} object.
     */
    Map<String, Object> serializeToXdm();
}
```

By implementing the **Property** interface, you can define complex properties for your XDM Schema. A complex property is defined as not being a primitive type, String, or Date.

```java
public interface Property {

    /**
     * Serialize this {@code Property} object to a map with the same format as its XDM schema.
     * @return XDM-formatted map of this {@code Property} object.
     */
    Map<String, Object> serializeToXdm();
}
```

When defining your custom XDM Schema\(s\), implement these interfaces to ensure that the AEP Edge extension successfully serializes the provided data before sending it to Adobe Experience Edge Network.

#### EdgeEventHandle

```java
/**
 * The {@link EdgeEventHandle} is a response fragment from Adobe Experience Edge Service for a sent XDM Experience Event.
 * One event can receive none, one or multiple {@link EdgeEventHandle}(s) as response.
 */
public class EdgeEventHandle {
  /**
     * @return the payload type or null if not found in the {@link JSONObject} response
     */
  public String getType() {...}

  /**
     * @return the event payload values for this {@link EdgeEventHandle} or null if not found in the {@link JSONObject} response
     */
  public List<Map<String, Object>> getPayload() {...}
}
```

Use this class when calling the sendEvent API with EdgeCallback.
{% endtab %}
{% endtabs %}

