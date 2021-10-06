# API Reference

## clearPropositions

This API clears out the client-side in-memory propositions cache.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void clearCachedPropositions()
```

#### Example

```java
Optimize.clearCachedPropositions();
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
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

The `extensionVersion()` method (on Android) or the `extensionVersion` property (on iOS) return the version information for currently installed AEPOptimize extension.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static String extensionVersion()
```

#### Example

```java
Optimize.extensionVersion();
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
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

This API retrieves the previously fetched propositions, for the provided decision scopes, from the in-memory extension propositions cache. The completion callback is invoked with the decision propositions corresponding to the given decision scopes. If a certain decision scope has not already been fetched prior to this API call, it will not be contained in the returned propositions.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void getPropositions(final List<DecisionScope> decisionScopes, final AdobeCallback<Map<DecisionScope, Proposition>> callback)
```

* _decisionScopes_ is a List of decision scopes for which propositions are requested.
* _callback_ `call` method is invoked with propositions map of type `Map<DecisionScope, Proposition>`. If callback is an instance of [AdobeCallbackWithError](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/mobile-core-api-reference#adobecallbackwitherror), and if the operation times out or an error occurs in retrieving propositions, `fail` method is invoked with the appropriate [AdobeError](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/mobile-core-api-reference#adobeerror).

#### Example

```java
final DecisionScope decisionScope1 = DecisionScope("xcore:offer-activity:1111111111111111", "xcore:offer-placement:1111111111111111", 2);
final DecisionScope decisionScope2 = new DecisionScope("myScope");

final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope1);
decisionScopes.add(decisionScope2);

Optimize.getPropositions(scopes, new AdobeCallbackWithError<Map<DecisionScope, Proposition>>() {
    @Override
    public void fail(final AdobeError adobeError) {
        // handle error
    }

    @Override
    public void call(Map<DecisionScope, Proposition> propositionsMap) {
        if (propositionsMap != null && !propositionsMap.isEmpty()) {
            // get the propositions for the given decision scopes
            if (propositionsMap.contains(decisionScope1)) {
                final Proposition proposition1 = propsMap.get(decisionScope1)
                // read proposition1 offers
            }
            if (propositionsMap.contains(decisionScope2)) {
                final Proposition proposition2 = propsMap.get(decisionScope2)
                // read proposition2 offers
            }
        }
    }
});
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
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
              completion: (void (^ _Nonnull)(NSDictionary<AEPDecisionScope*, AEPProposition*>* _Nullable propositionsDict, NSError* _Nullable error)) completion;
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
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void onPropositionsUpdate(final AdobeCallback<Map<DecisionScope, Proposition>> callback)
```

* _callback_ `call` method is invoked with propositions map of type `Map<DecisionScope, Proposition>`. If callback is an instance of `AdobeCallbackWithError`, and if the operation times out or an error occurs in retrieving propositions, `fail` method is invoked with the appropriate `AdobeError`.

#### Example

```java
Optimize.onPropositionsUpdate(new AdobeCallbackWithError<Map<DecisionScope, Proposition>>() {
    @Override
    public void fail(final AdobeError adobeError) {
        // handle error
    }

    @Override
    public void call(final Map<DecisionScope, Proposition> propositionsMap) {
        if (propositionsMap != null && !propositionsMap.isEmpty()) {
            // handle propositions
        }
    }
});
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
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
+ (void) onPropositionsUpdate: (void (^ _Nonnull)(NSDictionary<AEPDecisionScope*, AEPProposition*>* _Nullable)) action;
```

#### Example

```objc
[AEPMobileOptimize onPropositionsUpdate: ^(NSDictionary<AEPDecisionScope*, AEPProposition*>* propositionsDict) {
  // handle propositions
}];
```

{% endtab %}
{% endtabs %}

## registerExtension(s)

This API can be invoked to register the Optimize extension with the Mobile Core. On iOS, `registerExtensions` API is part of Mobile Core.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void registerExtension()
```

#### Example

```java
Optimize.registerExtension();
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
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
                 completion: (void (^ _Nullable)(void)) completion;
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

This `MobileCore` API can also be invoked to clear out the client-side data for the Optimize extension, such as the in-memory propositions cache.
For details on syntax, usage and availability, refer to [Mobile Core - Reset identities](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/mobile-core-api-reference#reset-identities).

## updatePropositions

This API dispatches an Event for the Edge network extension to fetch decision propositions, for the provided decision scopes array, from the decisioning services enabled in the Experience Edge. The returned decision propositions are cached in-memory in the Optimize SDK extension and can be retrieved using `getPropositions` API.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void updatePropositions(final List<DecisionScope> decisionScopes, final Map<String, Object> xdm, final Map<String, Object> data)
```

* _decisionScopes_ is a List of decision scopes for which propositions need updating.
* _xdm_ additional xdm formatted data to be attached to the Experience Event.
* _data_ additional freeform data to be attached to the Experience Event.

#### Example

```java
Optimize.updatePropositions(new AdobeCallbackWithError<Map<DecisionScope, Proposition>>() {
    @Override
    public void fail(final AdobeError adobeError) {
        // handle error
    }

    @Override
    public void call(final Map<DecisionScope, Proposition> propositionsMap) {
        if (propositionsMap != null && !propositionsMap.isEmpty()) {
            // handle propositions
        }
    }
});
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}
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

| Type | Android | (AEP 3.x) Swift | (AEP 3.x) Objective-C |
| :--- | :--- | :--- | :--- |
| class | `DecisionScope` | `AEPDecisionScope` |
| class | `Proposition` | `Proposition` | `AEPProposition` |
| class | `Offer` | `Offer` | `AEPOffer` |

### DecisionScope

This class represents the decision scope which is used to fetch the decision propositions from the Edge decisioning services. The encapsulated scope name can also represent the Base64-encoded JSON string created using the provided activityId, placementId, and itemCount.

{% tabs %}
{% tab title="Android" %}
#### Java

```java
/**
 * {@code DecisionScope} class represents a scope used to fetch personalized offers from the Experience Edge network.
 */
public class DecisionScope {

    /**
     * Constructor creates a {@code DecisionScope} using the provided {@code name}.
     *
     * @param name {@link String} containing scope name.
     */
    public DecisionScope(final String name) {...}

    /**
     * Constructor creates a {@code DecisionScope} using the provided {@code activityId} and {@code placementId}.
     * <p>
     * This constructor assumes the item count for the given scope to be {@value #DEFAULT_ITEM_COUNT}.
     *
     * @param activityId {@link String} containing activity identifier for the given scope.
     * @param placementId {@code String} containing placement identifier for the given scope.
     */
    public DecisionScope(final String activityId, final String placementId) {...}

    /**
     * Constructor creates a {@code DecisionScope} using the provided {@code activityId} and {@code placementId}.
     *
     * @param activityId {@link String} containing activity identifier for the given scope.
     * @param placementId {@code String} containing placement identifier for the given scope.
     * @param itemCount {@code String} containing number of items to be returned for the given scope.
     */
    public DecisionScope(final String activityId, final String placementId, final int itemCount) {...}

    /**
     * Gets the name for this scope.
     *
     * @return {@link String} containing the scope name.
     */
    public String getName() {...}
}
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}

#### Swift

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
    public init(name: String) {...}

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
    public convenience init(activityId: String, placementId: String, itemCount: UInt = 1) {...}
}
```
{% endtab %}
{% endtabs %}

### Proposition

This class represents the decision propositions received from the decisioning services, upon a personalization query request to the Experience Edge network.

{% tabs %}
{% tab title="Android" %}

#### Java

```java
public class Proposition {

    /**
     * Constructor creates a {@code Proposition} using the provided propostion {@code id}, {@code offers}, {@code scope} and {@code scopeDetails}.
     *
     * @param id {@link String} containing proposition identifier.
     * @param offers {@code List<Offer>} containing proposition items.
     * @param scope {@code String} containing encoded scope.
     * @param scopeDetails {@code Map<String, Object>} containing scope details.
     */
    Proposition(final String id, final List<Offer> offers, final String scope, final Map<String, Object> scopeDetails) {...}

    /**
     * Gets the {@code Proposition} identifier.
     *
     * @return {@link String} containing the {@link Proposition} identifier.
     */
    public String getId() {...}

    /**
     * Gets the {@code Proposition} items.
     *
     * @return {@code List<Offer>} containing the {@link Proposition} items.
     */
    public List<Offer> getOffers() {...}

    /**
     * Gets the {@code Proposition} scope.
     *
     * @return {@link String} containing the encoded {@link Proposition} scope.
     */
    public String getScope() {...}

    /**
     * Gets the {@code Proposition} scope details.
     *
     * @return {@code Map<String, Object>} containing the {@link Proposition} scope details.
     */
    public Map<String, Object> getScopeDetails() {...}

    /**
     * Generates a map containing XDM formatted data for {@code Experience Event - Proposition Reference} field group from this {@code Proposition}.
     * <p>
     * The returned XDM data does not contain {@code eventType} for the Experience Event.
     *
     * @return {@code Map<String, Object>} containing the XDM data for the proposition reference.
     */
    public Map<String, Object> generateReferenceXdm() {...}
}
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}

#### Swift

```swift
/// `Proposition` class
@objc(AEPProposition)
public class Proposition: NSObject, Codable {

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

#### Swift

```swift
/// `Proposition` extension
@objc
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
{% endtab %}
{% endtabs %}

### Offer

This class represents the proposition option received from the decisioning services, upon a personalization query to the Experience Edge network.

{% tabs %}
{% tab title="Android" %}

#### Java

```java
public class Offer {

    /**
     * {@code Offer} Builder.
     */
    public static class Builder {
        
        /**
        * Builder constructor with required {@code Offer} attributes as parameters.
        * <p>
        * It sets default values for remaining {@link Offer} attributes.
        *
        * @param id required {@link String} containing {@code Offer} identifier.
        * @param type required {@link OfferType} indicating the {@code Offer} type.
        * @param content required {@code String} containing the {@code Offer} content.
        */
        public Builder(final String id, final OfferType type, final String content) {...}

        /**
        * Sets the etag for this {@code Offer}.
        *
        * @param etag {@link String} containing {@link Offer} etag.
        * @return this Offer {@link Builder}
        * @throws UnsupportedOperationException if this method is invoked after {@link Builder#build()}.
        */
        public Builder setEtag(final String etag) {...}

        /**
        * Sets the schema for this {@code Offer}.
        *
        * @param schema {@link String} containing {@link Offer} schema.
        * @return this Offer {@link Builder}
        * @throws UnsupportedOperationException if this method is invoked after {@link Builder#build()}.
        */
        public Builder setSchema(final String schema) {...} 

        /**
        * Sets the language for this {@code Offer}.
        *
        * @param language {@code List<String>} containing supported {@link Offer} language.
        * @return this Offer {@link Builder}
        * @throws UnsupportedOperationException if this method is invoked after {@link Builder#build()}.
        */
        public Builder setLanguage(final List<String> language) {...}

        /**
        * Sets the characteristics for this {@code Offer}.
        *
        * @param characteristics {@code Map<String, String>} containing {@link Offer} characteristics.
        * @return this Offer {@link Builder}
        * @throws UnsupportedOperationException if this method is invoked after {@link Builder#build()}.
        */
        public Builder setCharacteristics(final Map<String, String> characteristics) {...}

        /**
        * Builds and returns the {@code Offer} object.
        *
        * @return {@link Offer} object or null.
        * @throws UnsupportedOperationException if this method is invoked after {@link Builder#build()}.
        */
        public Offer build() {...}
    }

    /**
     * Gets the {@code Offer} identifier.
     *
     * @return {@link String} containing the {@link Offer} identifier.
     */
    public String getId() {...}

    /**
     * Gets the {@code Offer} etag.
     *
     * @return {@link String} containing the {@link Offer} etag.
     */
    public String getEtag() {...}

    /**
     * Gets the {@code Offer} schema.
     *
     * @return {@link String} containing the {@link Offer} schema.
     */
    public String getSchema() {...}

    /**
     * Gets the {@code Offer} type.
     *
     * @return {@link OfferType} indicating the {@link Offer} type.
     */
    public OfferType getType() {...}

    /**
     * Gets the {@code Offer} language.
     *
     * @return {@code List<String>} containing the supported {@link Offer} language.
     */
    public List<String> getLanguage() {...}

    /**
     * Gets the {@code Offer} content.
     *
     * @return {@link String} containing the {@link Offer} content.
     */
    public String getContent() {...}

    /**
     * Gets the {@code Offer} characteristics.
     *
     * @return {@code Map<String, String>} containing the {@link Offer} characteristics.
     */
    public Map<String, String> getCharacteristics() {...}

    /**
     * Gets the containing {@code Proposition} for this {@code Offer}.
     *
     * @return {@link Proposition} instance.
     */
    public Proposition getProposition() {...}

    /**
     * Dispatches an event for the Edge network extension to send an Experience Event to the Edge network with the display interaction data for the
     * given {@code Proposition} offer.
     */
    public void displayed() {...}

    /**
     * Dispatches an event for the Edge network extension to send an Experience Event to the Edge network with the tap interaction data for the
     * given {@code Proposition} offer.
     */
    public void tapped() {...}

    /**
     * Generates a map containing XDM formatted data for {@code Experience Event - Proposition Interactions} field group from this {@code Proposition} item.
     * <p>
     * The returned XDM data does contain the {@code eventType} for the Experience Event with value {@code decisioning.propositionDisplay}.
     * <p>
     * Note: The Edge sendEvent API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, and override
     * dataset identifier.
     *
     * @return {@code Map<String, Object>} containing the XDM data for the proposition interaction.
     */
    public Map<String, Object> generateDisplayInteractionXdm() {...}

    /**
     * Generates a map containing XDM formatted data for {@code Experience Event - Proposition Interactions} field group from this {@code Proposition} offer.
     * <p>
     * The returned XDM data contains the {@code eventType} for the Experience Event with value {@code decisioning.propositionInteract}.
     * <p>
     * Note: The Edge sendEvent API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, and override
     * dataset identifier.
     *
     * @return {@code Map<String, Object>} containing the XDM data for the proposition interaction.
     */
    public Map<String, Object> generateTapInteractionXdm() {...}

}
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}

#### Swift

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
}
```

The `Offer` class extension provides methods for generating XDM data for Proposition Interactions field group which can be used for proposition tracking. It also contains direct methods for tracking proposition display and tap interactions.

#### Swift

```swift
/// `Offer` extension
@objc
public extension Offer {
    /// Creates a dictionary containing XDM formatted data for `Experience Event - Proposition Interactions` field group from the given proposition option.
    ///
    /// The Edge `sendEvent(experienceEvent:_:)` API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, or override dataset identifier.
    /// If the proposition reference within the option is released and no longer valid, the method returns `nil`.
    ///
    /// - Note: The returned XDM data also contains the `eventType` for the Experience Event with value `decisioning.propositionDisplay`.
    /// - Returns A dictionary containing XDM data for the propositon interactions.
    func generateDisplayInteractionXdm() -> [String: Any]? {...}

    /// Creates a dictionary containing XDM formatted data for `Experience Event - Proposition Interactions` field group from the given proposition option.
    ///
    /// The Edge `sendEvent(experienceEvent:_:)` API can be used to dispatch this data in an Experience Event along with any additional XDM, free-form data, or override dataset identifier.
    /// If the proposition reference within the option is released and no longer valid, the method returns `nil`.
    ///
    /// - Note: The returned XDM data also contains the `eventType` for the Experience Event with value `decisioning.propositionInteract`.
    /// - Returns A dictionary containing XDM data for the propositon interactions.
    func generateTapInteractionXdm() -> [String: Any]? {...}

    /// Dispatches an event for the Edge extension to send an Experience Event to the Edge network with the display interaction data for the given proposition item.
    func displayed() {...}

    /// Dispatches an event for the Edge extension to send an Experience Event to the Edge network with the tap interaction data for the given proposition item.
    func tapped() {...}
}
```
{% endtab %}
{% endtabs %}

### OfferType

An enum indicating the type of an offer, derived from the proposition item `format` field in personalization query response.

{% tabs %}
{% tab title="Android" %}

#### Java

```java
public enum OfferType {
    UNKNOWN, JSON, TEXT, HTML, IMAGE;

    @Override
    public String toString() {...}

    /**
     * Returns the {@code OfferType} for the given {@code format}.
     *
     * @param format {@link String} containing the {@link Offer} format.
     * @return {@link OfferType} indicating the {@code Offer} format.
     */
    public static OfferType from(final String format) {...}
}
```
{% endtab %}
{% tab title="iOS (AEP 3.x)" %}

#### Swift

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
    init(from format: String) {...}
}
```

{% endtab %}
{% endtabs %}

