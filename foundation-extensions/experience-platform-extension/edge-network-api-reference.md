# Edge Network API reference

## extensionVersion

Returns the version of the client-side Edge extension.

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static String extensionVersion();
```

**Example**

```java
String extensionVersion = Edge.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

**Syntax**

```swift
static let extensionVersion
```

**Example**

```swift
let extensionVersion = Edge.extensionVersion
```

### Objective-C

**Syntax**

```objectivec
+ (nonnull NSString*) extensionVersion;
```

**Example**

```objectivec
NSString *extensionVersion = [AEPMobileEdge extensionVersion];
```
{% endtab %}
{% endtabs %}

## sendEvent

Sends an Experience event to Adobe Experience Platform Edge Network.

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static void sendEvent(final ExperienceEvent experienceEvent, final EdgeCallback callback);
```
* _experienceEvent_ - the XDM [Experience Event](edge-network-api-reference.md#experienceevent) to be sent to Adobe Experience Platform Edge Network
* _completion_ - optional callback to be invoked when the request is complete, returning the associated [EdgeEventHandle(s)](edge-network-api-reference.md#edgeeventhandle) received from the Adobe Experience Platform Edge Network. It may be invoked on a different thread.

**Example**

```java
// create experience event from Map
Map<String, Object> xdmData = new HashMap<>();
xdmData.put("eventType", "SampleXDMEvent");
xdmData.put("sample", "data");
		
ExperienceEvent experienceEvent = new ExperienceEvent.Builder()
	.setXdmSchema(xdmData)
	.build();
```
```java
// example 1 - send the experience event without handling the Edge Network response
Edge.sendEvent(experienceEvent, null);
```
```java
// example 2 - send the experience event and handle the Edge Network response onComplete
Edge.sendEvent(experienceEvent, new EdgeCallback() {
  @Override
  public void onComplete(final List<EdgeEventHandle> handles) {
        // handle the Edge Network response 
  }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

**Syntax**

```swift
static func sendEvent(experienceEvent: ExperienceEvent, _ completion: (([EdgeEventHandle]) -> Void)? = nil)
```

* _experienceEvent_ - the XDM [Experience Event](edge-network-api-reference.md#experienceevent) to be sent to Adobe Experience Platform Edge Network
* _completion_ - optional callback to be invoked when the request is complete, returning the associated [EdgeEventHandle(s)](edge-network-api-reference.md#edgeeventhandle) received from the Adobe Experience Platform Edge Network. It may be invoked on a different thread.

**Example**

```swift
//create experience event from dictionary:
var xdmData : [String: Any] = ["eventType" : "SampleXDMEvent",
                              "sample": "data"]
let experienceEvent = ExperienceEvent(xdm: xdmData)
```
```swift
// example 1 - send the experience event without handling the Edge Network response
Edge.sendEvent(experienceEvent: experienceEvent)
```

```swift
// example 2 - send the experience event and handle the Edge Network response onComplete
Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
            // handle the Edge Network response
        }
```

### Objective-C

**Syntax**

```objectivec
+ (void) sendExperienceEvent:(AEPExperienceEvent * _Nonnull) completion:^(NSArray<AEPEdgeEventHandle *> * _Nonnull)completion
```

**Example**
```objectivec
//create experience event from dictionary:
NSDictionary *xdmData = @{ @"eventType" : @"SampleXDMEvent"};
NSDictionary *data = @{ @"sample" : @"data"};
```

```objectivec
// example 1 - send the experience event without handling the Edge Network response
[AEPMobileEdge sendExperienceEvent:event completion:nil];
```
```objectivec
// example 2 - send the experience event and handle the Edge Network response onComplete
[AEPMobileEdge sendExperienceEvent:event completion:^(NSArray<AEPEdgeEventHandle *> * _Nonnull handles) {
  // handle the Edge Network response
}];
```
{% endtab %}
{% endtabs %}

## registerExtension

Registers the Edge extension with the Mobile Core SDK.

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static void registerExtension();
```

**Example**

```java
Edge.registerExtension();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

Use the MobileCore API to register the Edge extension.

**Syntax**

```swift
// MobileCore
public static func registerExtensions(_ extensions: [Extension.Type], _ completion: (() -> Void)? = nil)
```

**Example**

```swift
import AEPEdge

...
MobileCore.registerExtensions([Edge.self, ...], {
  // processing after registration
})
```

### Objective-C

Use the AEPMobileCore API to register the Edge extension.

**Syntax**

```objectivec
+ (void) registerExtensions: (NSArray<Class*>* _Nonnull) extensions 
                  completion: (void (^ _Nullable)(void)) completion;
```

**Example**

```objectivec
@import AEPEdge;

[AEPMobileCore registerExtensions:@[AEPMobileEdge.class] completion:nil];...

```

{% endtab %}
{% endtabs %}

## resetIdentities

Resets current state of the AEP Edge extension and clears previously cached content related to current identity, if any.

See [MobileCore.resetIdentities](../mobile-core/mobile-core-api-reference.md#resetidentities) for more details.

## Public classes

### XDM Schema

The AEP Edge extension provides the Schema and Property interfaces (Android) / XDMSchema protocol (iOS) that can be used to define the classes associated with your XDM schema in Adobe Experience Platform.

{% tabs %}
{% tab title="Android" %}

### Java

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
When defining your custom XDM schema(s), implement these interfaces to ensure that the AEP Edge extension successfully serializes the provided data before sending it to Adobe Experience Platform Edge Network.

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

```swift
/// An interface representing a Platform XDM Event Data schema.
public protocol XDMSchema: Encodable {

    /// Returns the version of this schema as defined in the Adobe Experience Platform.
    /// - Returns: The version of this schema
    var schemaVersion: String { get }

    /// Returns the identifier for this schema as defined in the Adobe Experience Platform.
    /// The identifier is a URI where this schema is defined.
    /// - Returns: The URI identifier for this schema
    var schemaIdentifier: String { get }

    /// Returns the identifier for this dataset as defined in the Adobe Experience Platform.
    /// This is a system generated identifier for the Dataset the event belongs to.
    /// - Returns: The  identifier as a String for this dataset
    var datasetIdentifier: String { get }
}
```
{% endtab %}
{% endtabs %}

### EdgeEventHandle

The `EdgeEventHandle` is a response fragment from Adobe Experience Platform Edge Network for a sent XDM Experience Event.
One event can receive none, one or multiple `EdgeEventHandle`(s) as response.

{% tabs %}
{% tab title="Android" %}
### Java

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

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

```swift
@objc(AEPEdgeEventHandle)
public class EdgeEventHandle: NSObject, Codable {
    /// Payload type
    @objc public let type: String?

    /// Event payload values
    @objc public let payload: [[String: Any]]?
}
```
{% endtab %}
{% endtabs %}

Use this class when calling the [sendEvent](edge-network-api-reference.md#sendevent) API with EdgeCallback.

### ExperienceEvent

Experience Event is the event to be sent to Adobe Experience Platform Edge Network.
The XDM data is required for any Experience Event being sent using the Edge extension.

{% tabs %}
{% tab title="Android" %}

### Java

```Java
public final class ExperienceEvent {

  public static class Builder {
    ...

    public Builder() {
      ...
    }

    /**
      * Sets free form data associated with this event to be passed to Adobe Experience Edge.
      *
      * @param data free form data, JSON like types are accepted
      * @return instance of current builder
      * @throws UnsupportedOperationException if this instance was already built
      */
    public Builder setData(final Map<String, Object> data) {...}

    /**
      * Solution specific XDM event data for this event.
      *
      * @param xdm {@link Schema} information
      * @return instance of current builder
      * @throws UnsupportedOperationException if this instance was already built
      */
    public Builder setXdmSchema(final Schema xdm) {...}

    /**
      * Solution specific XDM event data and dataset identifier for this event.
      *
      * @param xdm {@code Map<String, Object>} of raw XDM schema data
      * @param datasetIdentifier The Experience Platform dataset identifier where this event is sent.
      *                          If not provided, the default dataset defined in the configuration ID is used
      * @return instance of current builder
      * @throws UnsupportedOperationException if this instance was already built
      */
    public Builder setXdmSchema(final Map<String, Object> xdm, final String datasetIdentifier) {...}

    /**
      * Solution specific XDM event data for this event, passed as raw mapping of keys and
      * Object values.
      *
      * @param xdm {@code Map<String, Object>} of raw XDM schema data
      * @return instance of current builder
      * @throws UnsupportedOperationException if this instance was already built
      */
    public Builder setXdmSchema(final Map<String, Object> xdm) {...}

    /**
      * Builds and returns a new instance of {@code ExperienceEvent}.
      *
      * @return a new instance of {@code ExperienceEvent} or null if one of the required parameters is missing
      * @throws UnsupportedOperationException if this instance was already built
      */
    public ExperienceEvent build() {...}
  }

  public Map<String, Object> getData() {...}

  public Map<String, Object> getXdmSchema() {...} 
}  
```

**Examples**

```java
//Example 1
// set freeform data to the Experience event
Map<String, Object> xdmData = new HashMap<>();
xdmData.put("eventType", "SampleXDMEvent");
xdmData.put("sample", "data");

Map<String, Object> data = new HashMap<>();
data.put("free", "form");
data.put("data", "example");

ExperienceEvent experienceEvent = new ExperienceEvent.Builder()
  .setXdmSchema(xdmData)
  .setData(data)
  .build();
```

```java
//Example 2
// Create Experience Event from XDM Schema implementations
public class XDMSchemaExample implements com.adobe.marketing.mobile.xdm.Schema {
  private String eventType;
  private String otherField;
      ...

      public String getEventType() {
        return this.eventType;
      }

      public void setEventType(final String newValue) {
        this.eventType = newValue;
      }

      public String getOtherField() {
        return this.otherField;
      }

      public void setOtherField(final String newValue) {
        this.otherField = newValue;
      }
      }

// Create Experience Event from Schema
XDMSchemaExample xdmData = new XDMSchemaExample();
xdmData.setEventType("SampleXDMEvent");
xdmData.setOtherField("OtherFieldValue");

ExperienceEvent experienceEvent = new ExperienceEvent.Builder()
  .setXdmSchema(xdmData)
  .build();
```

```java
//Example 3
// Set the destination Dataset identifier to the current Experience event:
Map<String, Object> xdmData = new HashMap<>();
xdmData.put("eventType", "SampleXDMEvent");
xdmData.put("sample", "data");

ExperienceEvent experienceEvent = new ExperienceEvent.Builder()
  .setXdmSchema(xdmData, "datasetIdExample")
  .build();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

```swift
@objc(AEPExperienceEvent)
public class ExperienceEvent: NSObject {

    /// XDM formatted data, use an `XDMSchema` implementation for a better XDM data injection and format control
    @objc public let xdm: [String: Any]?

    /// Optional free-form data associated with this event
    @objc public let data: [String: Any]?

    /// Adobe Experience Platform dataset identifier, if not set the default dataset identifier set in the Edge Configuration is used
    @objc public let datasetIdentifier: String?

    /// Initialize an Experience Event with the provided event data
    /// - Parameters:
    ///   - xdm:  XDM formatted data for this event, passed as a raw XDM Schema data dictionary.
    ///   - data: Any free form data in a [String : Any] dictionary structure.
    ///   - datasetIdentifier: The Experience Platform dataset identifier where this event should be sent to; if not provided, the default dataset identifier set in the Edge configuration is used
    @objc public init(xdm: [String: Any], data: [String: Any]? = nil, datasetIdentifier: String? = nil) {...}

    /// Initialize an Experience Event with the provided event data
    /// - Parameters:
    ///   - xdm: XDM formatted event data passed as an XDMSchema
    ///   - data: Any free form data in a [String : Any] dictionary structure.
    public init(xdm: XDMSchema, data: [String: Any]? = nil) {...}
}

```
### Swift

**Examples**

```swift
//Example 1
// set freeform data to the Experience event
var xdmData : [String: Any] = ["eventType" : "SampleXDMEvent",
                              "sample": "data"]

let experienceEvent = ExperienceEvent(xdm: xdmData, data: ["free": "form", "data": "example"])
```

```swift
//Example 2
// Create Experience Event from XDM Schema implementations
import AEPEdge

public struct XDMSchemaExample : XDMSchema {
    public let schemaVersion = "1.0" // Returns the version of this schema as defined in the Adobe Experience Platform.
    public let schemaIdentifier = "" // The URI identifier for this schema
    public let datasetIdentifier = "" // The identifier for the Dataset this event belongs to.

    public init() {}

    public var eventType: String?
    public var otherField: String?

    enum CodingKeys: String, CodingKey {
    case eventType = "eventType"
    case otherField = "otherField"
    }		
}

extension XDMSchemaExample {
    public func encode(to encoder: Encoder) throws {
      var container = encoder.container(keyedBy: CodingKeys.self)
      if let unwrapped = eventType { try container.encode(unwrapped, forKey: .eventType) }
      if let unwrapped = otherField { try container.encode(unwrapped, forKey: .otherField) }
    }
}

...

// Create Experience Event from XDMSchema
var xdmData = XDMSchemaExample()
xdmData.eventType = "SampleXDMEvent"
xdm.otherField = "OtherFieldValue"
let event = ExperienceEvent(xdm: xdmData)
```

```swift
//Example 3
// Set the destination Dataset identifier to the current Experience event:
var xdmData : [String: Any] = ["eventType" : "SampleXDMEvent",
                              "sample": "data"]

let experienceEvent = ExperienceEvent(xdm: xdmData, datasetIdentifier: "datasetIdExample")
```

### Objective-C

**Examples**

```objectivec
//Example 1
// set freeform data to the Experience event
NSDictionary *xdmData = @{ @"eventType" : @"SampleXDMEvent"};
NSDictionary *data = @{ @"sample" : @"data"};
    
    AEPExperienceEvent *event = [[AEPExperienceEvent alloc] initWithXdm:xdmData data:data datasetIdentifier:nil];
```
```objectivec
//Example 2
// Set the destination Dataset identifier to the current Experience event:
NSDictionary *xdmData = @{ @"eventType" : @"SampleXDMEvent"};
   
AEPExperienceEvent *event = [[AEPExperienceEvent alloc] initWithXdm:xdmData data:nil datasetIdentifier:@"datasetIdExample"];
```
{% endtab %}
{% endtabs %}

See [Edge Extension Usage](https://github.com/adobe/aepsdk-edge-ios/blob/main/docs/ExtensionUsage.md) for more examples.
