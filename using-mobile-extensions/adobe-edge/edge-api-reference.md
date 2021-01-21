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



## Public classes

{% tabs %}
{% tab title="Android" %}

#### Java

##### Schema and Property interfaces

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

By implementing the **Property** interface, you can define complex properties for your XDM Schema. A complex property is defined as not being a primitive type, string, or date.

```java
public interface Property {

    /**
     * Serialize this {@code Property} object to a map with the same format as its XDM schema.
     * @return XDM-formatted map of this {@code Property} object.
     */
    Map<String, Object> serializeToXdm();
}
```

When defining your custom XDM Schema(s), implement these interfaces to ensure that the AEP Edge extension successfully serializes the provided data before sending it to Adobe Experience Edge Network.

##### EdgeEventHandle

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

Use this class with when calling the sendEvent API with EdgeCallback.

{% endtab %}

{% tab title="iOS" %}

#### Swift

##### XDMSchema protocol

When using the AEPEdge extension, the **XDMSchema** protocol can be implemented to define the classes that are associated with your defined schema in Adobe Experience Platform.

```swift
import Foundation

/// An protocol representing an Experience XDM Event Data schema.
public protocol XDMSchema: Encodable {

    /// Returns the version of this schema as defined in the Adobe Experience Platform.
    /// - Returns: The version of this schema
    var schemaVersion: String { get }

    /// Returns the identifier for this schema as defined in the Adobe Experience Platform.
    /// The identifier is a URI where this schema is defined.
    /// - Returns: The URI identifier for this schema
    var schemaIdentifier:  String { get }

    /// Returns the identifier for this dataset as defined in the Adobe Experience Platform.
    /// This is a system generated identifier for the Dataset the event belongs to.
    /// - Returns: The  identifier as a String for this dataset
    var datasetIdentifier: String { get }
}

extension XDMSchema {
    func toJSONData() -> Data? {
        try? JSONEncoder().encode(self)
    }
}
```

By implementing this **XDMSchema** protocol, you can define complex properties for your XDM Schema. A complex property is defined as not being a fundamental type \(Int, Float, Double, Bool or String\), or Date.

When defining your custom XDM Schema(s), implement this protocol to ensure that the AEP Edge extension successfully serializes the provided data before sending it to Adobe Experience Edge Network.

##### EdgeEventHandle

```swift
/// The EdgeEventHandle is a response fragment from Adobe Experience Edge Service for a sent XDM Experience Event. 
/// One event can receive none, one or multiple `EdgeEventHandle`(s) as response.
public class EdgeEventHandle: NSObject, Codable {

    /// Payload type
    public let type: String?

    /// Event payload values
    public let payload: [[String: Any]]?
}
```

Use this class when calling the sendEvent API with completion handler.

{% endtab %}
{% endtabs %}

