# API Reference

## clearPropositions

This API clears out the client-side in-memory propositions cache.

{% tabs %}
{% tab title="iOS — Swift" %}
### Swift

#### Syntax

```swift
static func clearCachedPropositions()
```

#### Example

```swift
Optimize.clearCachedPropositions()
```

### Objective-C

#### Syntax

```objc
+ (void) clearCachedPropositions;
```

#### Example

```objc
[AEPMobileOptimize clearCachedPropositions];
```

{% endtab %}
{% endtabs %}

## extensionVersion

This property contains the version information for currently installed AEPOptimize extension.

{% tabs %}
{% tab title="iOS — Swift" %}
### Swift

#### Syntax

```swift
static var extensionVersion: String
```

#### Example

```swift
let extensionVersion = Optimize.extensionVersion
```

### Objective-C

#### Syntax

```objc
+ (nonnull NSString*) extensionVersion;
```

#### Example

```objc
NSString *extensionVersion = [AEPMobileOptimize extensionVersion];
```

{% endtab %}
{% endtabs %}

## getPropositions

This API retrieves the previously fetched propositions, for the provided decision scopes, from the in-memory extension propositions cache. The completion handler is invoked with the decision propositions corresponding to the given decision scopes. If a certain decision scope has not already been fetched prior to this API call, it will not be contained in the returned propositions.

{% tabs %}
{% tab title="iOS — Swift" %}
### Swift

#### Syntax

```swift
static func getPropositions(for decisionScopes: [DecisionScope], 
                            _ completion: @escaping ([DecisionScope: Proposition]?, Error?) -> Void)
```

* _decisionScopes_ is an array of decision scopes for which propositions are requested.
* _completion_ is invoked with propositions dictionary of type `[DecisionScope: Proposition]`. An `Error` is returned if SDK fails to retrieve the propositions.

#### Example

```swift
let decisionScope1 = DecisionScope(activityId: "xcore:offer-activity:1111111111111111", 
                                   placementId: "xcore:offer-placement:1111111111111111" 
                                   itemCount: 2)
let decisionScope2 = DecisionScope(name: "myScope")

Optimize.getPropositions(for: [decisionScope1, decisionScope2]) { propositionsDict, error in

    if let error = error {
        // handle error
        return
    }

    if let propositionsDict = propositionsDict {
        // get the propositions for the given decision scopes

        if let proposition1 = propositionsDict[decisionScope1] {
            // read proposition1 offers
        }

        if let proposition2 = propositionsDict[decisionScope2] {
            // read proposition2 offers
        }
    }
}
```

### Objective-C

#### Syntax

```objc
+ (void) getPropositions: (NSArray<AEPDecisionScope*>* _Nonnull) decisionScopes 
              completion: (void (^)(NSDictionary<AEPDecisionScope*, AEPProposition*>* _Nullable propositionsDict, NSError* _Nullable error)) completion;
```

#### Example

```objc
AEPDecisionScope* decisionScope1 = [[AEPDecisionScope alloc] initWithActivityId: @"xcore:offer-activity:1111111111111111" 
                                                                   placementId: @"xcore:offer-placement:1111111111111111" 
                                                                     itemCount: 2];
AEPDecisionScope* decisionScope2 = [[AEPDecisionScope alloc] initWithName: @"myScope"];

[AEPMobileOptimize getPropositions: @[decisionScope1, decisionScope2] 
                        completion: ^(NSDictionary<AEPDecisionScope*, AEPProposition*>* propositionsDict, NSError* error) {
  if (error != nil) {
    // handle error   
    return;
  }

  AEPProposition* proposition1 = propositionsDict[decisionScope1];
  // read proposition1 offers

  AEPProposition* proposition2 = propositionsDict[decisionScope2];
  // read proposition2 offers
}];
```

{% endtab %}
{% endtabs %}

## onPropositionsUpdate

This API registers a permanent callback which is invoked whenever the Edge extension dispatches a response Event received from the Experience Edge Network upon a personalization query. The personalization query requests can be triggered by the `updatePropositions` API, Edge extension `sendEvent` API or launch consequence rules.

{% tabs %}
{% tab title="iOS — Swift" %}
### Swift

#### Syntax

```swift
static func onPropositionsUpdate(perform action: @escaping ([DecisionScope: Proposition]?) -> Void)
```

* _action_ is invoked with propositions dictionary of type `[DecisionScope: Proposition]`

#### Example

```swift
Optimize.onPropositionsUpdate { propositionsDict in
  if let propositionsDict = propositionsDict {
    // handle propositions
  }
}
```

### Objective-C

#### Syntax

```objc
+ (void) onPropositionsUpdate: (void (^)(NSDictionary<AEPDecisionScope*, AEPProposition*>* _Nullable)) action;
```

#### Example

```objc
[AEPMobileOptimize onPropositionsUpdate: ^(NSDictionary<AEPDecisionScope*, AEPProposition*>* propositionsDict) {
  // handle propositions
}];
```

{% endtab %}
{% endtabs %}

## registerExtension

This `MobileCore` API can be invoked to register the Optimize extension.

{% tabs %}
{% tab title="iOS — Swift" %}
### Swift

#### Syntax

```swift
static func registerExtensions(_ extensions: [NSObject.Type], 
                               _ completion: (() -> Void)? = nil)
```

#### Example

```swift
MobileCore.registerExtensions([Optimize.self, ...]) {
    // Processing upon registration completion
}
```

### Objective-C

#### Syntax

```objc
+ (void) registerExtensions: (NSArray<Class*>* _Nonnull) extensions 
                 completion: (void (^)(void)) completion;
```

#### Example

```objc
[AEPMobileCore registerExtensions:@[AEPMobileOptimize.class, ...] completion:^{
  // Processing upon registration completion
}];
```

{% endtab %}
{% endtabs %}

## resetIdentities

This `MobileCore` API can also be invoked to clear out the client-side data for Optimize extension, e.g. in-memory propositions cache.

{% tabs %}
{% tab title="iOS — Swift" %}
### Swift

#### Syntax

```swift
static func resetIdentities()
```

#### Example

```swift
MobileCore.resetIdentities()
```

### Objective-C

#### Syntax

```objc
+ (void) resetIdentities;
```

#### Example

```objc
[AEPMobileCore resetIdentities];
```

{% endtab %}
{% endtabs %}

## updatePropositions

This API dispatches an Event for the Edge network extension to fetch decision propositions, for the provided decision scopes array, from the decisioning services enabled in the Experience Edge. The returned decision propositions are cached in-memory in the Optimize SDK extension and can be retrieved using `getPropositions` API.

{% tabs %}
{% tab title="iOS — Swift" %}
### Swift

#### Syntax

```swift
static func updatePropositions(for decisionScopes: [DecisionScope], 
                               withXdm xdm: [String: Any]?,
                               andData data: [String: Any]? = nil)
```

* _decisionScopes_ is an array of decision scopes for which propositions need updating.
* _xdm_ additional xdm formatted data to be attached to the Experience Event.
* _data_ additional freeform data to be attached to the Experience Event.

#### Example

```swift
let decisionScope1 = DecisionScope(activityId: "xcore:offer-activity:1111111111111111", 
                                   placementId: "xcore:offer-placement:1111111111111111" 
                                   itemCount: 2)
let decisionScope2 = DecisionScope(name: "myScope")

Optimize.updatePropositions(for: [decisionScope1, decisionScope2] 
                            withXdm: ["xdmKey": "xdmValue"] 
                            andData: ["dataKey": "dataValue"])
```

### Objective-C

#### Syntax

```objc
+ (void) updatePropositions: (NSArray<AEPDecisionScope*>* _Nonnull) decisionScopes 
                    withXdm: (NSDictionary<NSString*, id>* _Nullable) xdm
                    andData: (NSDictionary<NSString*, id>* _Nullable) data;
```

#### Example

```objc
AEPDecisionScope* decisionScope1 = [[AEPDecisionScope alloc] initWithActivityId: @"xcore:offer-activity:1111111111111111" 
                                                                   placementId: @"xcore:offer-placement:1111111111111111" 
                                                                     itemCount: 2];
AEPDecisionScope* decisionScope2 = [[AEPDecisionScope alloc] initWithName: @"myScope"]; 

[AEPMobileOptimize updatePropositions: @[decisionScope1, decisionScope2] 
                              withXdm: @{@"xdmKey": @"xdmValue"} 
                              andData: @{@"dataKey": @"dataValue"}];
```

{% endtab %}
{% endtabs %}

## Public classes

| Type | Swift | Objective-C |
| :--- | :--- | :--- |
| class | `DecisionScope` | `AEPDecisionScope` |
| class | `Proposition` | `AEPProposition` |
| class | `Offer` | `AEPOffer` |

{% tabs %}
{% tab title="iOS — Swift" %}
### DecisionScope

This class represents the decision scope which is used to fetch the decision propositions from the Edge decisioning services. The encapsulated scope name can also represent the Base64 encoded JSON string created using the provided activityId, placementId and itemCount.

```swift
/// `DecisionScope` class is used to create decision scopes for personalization query requests to Experience Edge Network.
@objc(AEPDecisionScope)
public class DecisionScope: NSObject, Codable {
    /// Decision scope name
    @objc public let name: String

    /// Creates a new decision scope using the given scope `name`.
    ///
    /// - Parameter name: string representation for the decision scope.
    @objc
    public init(name: String) {
        self.name = name
    }

    /// Creates a new decision scope using the given `activityId`, `placementId` and `itemCount`.
    ///
    /// This initializer creates a scope name by Base64 encoding the JSON string created using the provided data.
    ///
    /// If `itemCount` == 1, JSON string is
    ///
    ///     {"activityId":#activityId,"placementId":#placementId}
    /// otherwise,
    ///
    ///     {"activityId":#activityId,"placementId":#placementId,"itemCount":#itemCount}
    /// - Parameters:
    ///   - activityId: unique activity identifier for the decisioning activity.
    ///   - placementId: unique placement identifier for the decisioning activity offer.
    ///   - itemCount: number of offers to be returned from the server.
    @objc
    public convenience init(activityId: String, placementId: String, itemCount: UInt = 1) {
        let name = "\(activityId: activityId, placementId: placementId, itemCount: itemCount)".base64Encode()

        self.init(name: name ?? "")
    }
}
```

### Proposition

This class represents the decision propositions received from the decisioning services, upon a personalization query request to the Experience Edge network.

```swift
/// `Proposition` class
@objc(AEPProposition)
public class Proposition: NSObject, Codable {
    private let items: [Offer]

    /// Unique proposition identifier
    @objc public let id: String

    /// Array containing proposition decision options
    @objc public lazy var offers: [Offer] = {...}()

    /// Decision scope string
    @objc public let scope: String

    /// Scope details dictionary
    @objc public var scopeDetails: [String: Any]
}
```

The `Proposition` class extension provides a method for generating XDM data for Proposition Reference field group which can be used for proposition tracking.

```swift
/// `Proposition` extension
public extension Proposition {
    /// Creates a dictionary containing XDM formatted data for `Experience Event - Proposition Reference` field group from the given proposition.
    ///
    /// The Edge `sendEvent(experienceEvent:_:)` API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, or override dataset identifier.
    ///
    /// - Note: The returned XDM data does not contain an `eventType` for the Experience Event.
    /// - Returns A dictionary containing XDM data for the propositon reference.
    func generateReferenceXdm() -> [String: Any] {...}
}
```

### Offer

This class represents the proposition option received from the decisioning services, upon a personalization query to the Experience Edge network.

```swift
/// `Offer` class
@objc(AEPOffer)
public class Offer: NSObject, Codable {
    /// Unique Offer identifier
    @objc public let id: String

    /// Offer revision detail at the time of the request
    @objc public let etag: String

    /// Offer schema string
    @objc public let schema: String

    /// Offer type as represented in enum `OfferType`
    @objc public let type: OfferType

    /// Optional Offer language array
    @objc public let language: [String]?

    /// Offer content string
    @objc public let content: String

    /// Optional Offer characteristics dictionary
    @objc public let characteristics: [String: String]?

    /// Weak reference to Proposition instance
    @objc weak var proposition: Proposition?
}
```

The `Offer` class extension provides methods for generating XDM data for Proposition Interactions field group which can be used for proposition tracking. It also contains direct methods for  tracking proposition display and tap interactions.

```swift
/// `Offer` extension
public extension Offer {
    /// Creates a dictionary containing XDM formatted data for `Experience Event - Proposition Interactions` field group from the given proposition option.
    ///
    /// The Edge `sendEvent(experienceEvent:_:)` API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, or override dataset identifier.
    ///
    /// - Note: The returned XDM data also contains the `eventType` for the Experience Event with value `display`.
    /// - Returns A dictionary containing XDM data for the propositon interactions.
    func generateDisplayInteractionXdm() -> [String: Any] {...}

    /// Creates a dictionary containing XDM formatted data for `Experience Event - Proposition Interactions` field group from the given proposition option.
    ///
    /// The Edge `sendEvent(experienceEvent:_:)` API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, or override dataset identifier.
    ///
    /// - Note: The returned XDM data also contains the `eventType` for the Experience Event with value `click`.
    /// - Returns A dictionary containing XDM data for the propositon interactions.
    func generateTapInteractionXdm() -> [String: Any] {...}

    /// Dispatches an event for the Edge extension to send an Experience Event to the Edge network with the display interaction data for the given proposition item.
    func displayed() {...}

    /// Dispatches an event for the Edge extension to send an Experience Event to the Edge network with the tap interaction data for the given proposition item.
    func tapped() {...}
}
```

### OfferType

An enum indicating the type of an Offer, derived from the proposition item `format` field in personalization query response.

```swift
/// Enum representing the supported Offer Types.
public enum OfferType: Int, Codable {

    /// Unknown Offer type
    case unknown = 0

    /// JSON Offer
    case json = 1

    /// Plain text Offer
    case text = 2

    /// Html Offer
    case html = 3

    /// Image Offer
    case image = 4

    /// Initializes OfferType with the provided format string.
    /// - Parameter format: Offer format string
    init(from format: String) {
        switch format {
        case "application/json":
            self = .json

        case "text/plain":
            self = .text

        case "text/html":
            self = .html

        default:
            self = format.starts(with: "image/") ? .image : .unknown
        }
    }
}
```

{% endtab %}
{% endtabs %}

