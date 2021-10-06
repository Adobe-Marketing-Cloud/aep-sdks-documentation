# API Reference

## onOfferUpdate

Use this API to register a callback, it will be invoked whenever the AEP Offer Decisioning extension receives an offer response from backend services. The Offer Decisioning requests can be triggered by the `OfferDecisioning.prefetchOffers()` API, `Edge.sendEvent()` API or consequence rules.

{% tabs %}
{% tab title="Android" %}
#### Syntax

```java
public static void onOfferUpdate(final AdobeCallbackWithError<Map<DecisionScope, List<Offer>>> callback)
```

#### Example

#### Java

```java
OfferDecisioning.onOfferUpdate(new AdobeCallbackWithError<Map<DecisionScope, List<Offer>>>() {
            @Override
            public void fail(AdobeError adobeError) {

            }
            @Override
            public void call(Map<DecisionScope, List<Offer>> decisionScopeListMap) {
                  // handle offers
            }
        });
```
{% endtab %}

{% tab title="iOS — Swift" %}
#### Syntax

```swift
func onOfferUpdate(perform: @escaping ([DecisionScope: [Offer]]) -> Void)
```

#### Example

Here are some examples in Objective C and Swift:

**Objective C**

```objectivec
[AEPMobileOfferDecisioning onOfferUpdateWithPerform:^(NSDictionary<AEPDecisionScope*, NSArray<AEPOffer*>*>* offersDict) {
//handle offers response
}];
```

**Swift**

```swift
OfferDecisioning.onOfferUpdate { offersDict in
//handle offers response
}
```
{% endtab %}
{% endtabs %}

## prefetchOffers

This API sends a request to the Offer Decisioning Services with the decisioning scopes array. The returned offers will be cached and you can use `retrievePrefetchedOffers` API to retrieve them later on demand.

{% tabs %}
{% tab title="Android" %}
#### Syntax

```java
public static void prefetchOffers(final List<DecisionScope> decisionScopes)
public static void prefetchOffers(final List<DecisionScope> decisionScopes, final OfferExperienceEvent offerExperienceEvent)
```

#### Example

#### Java

```java
// prefetch offers for decision scopes
OfferDecisioning.prefetchOffers(Arrays.asList(
                        new DecisionScope("xcore:offer-activity:124e8bc413c888dd", "xcore:offer-placement:124e8a16430888db")));

// prefetch offers for decision scopes with additional expxperience event
OfferExperienceEvent exEvent = new OfferExperienceEvent(
                        new HashMap<String, Object>() {
                            {
                                put("xdmkey", "xdmvalue");
                            }
                        },null,"override-datasetId");
OfferDecisioning.prefetchOffers(Arrays.asList(
                        new DecisionScope("xcore:offer-activity:124e8bc413c888dd", "xcore:offer-placement:124e8a16430888db"),
                        exEvent);
```
{% endtab %}

{% tab title="iOS — Swift" %}
#### Syntax

```swift
func prefetchOffers(decisionScopes: [DecisionScope], experienceEvent: OfferExperienceEvent? = nil)
```

#### Examples

Here are some examples in Objective C and Swift:

**Objective C**

```objectivec
AEPDecisionScope* decisionScope = [[AEPDecisionScope alloc] initWithActivityId:@"xcore:offer-activity:124e8bc413c888dd" placementId:@"xcore:offer-placement:124e8a16430888db"];

// prefetch offers for decision scopes
[AEPMobileOfferDecisioning prefetchOffersWithDecisionScopes:@[decisionScope]];

// prefetch offers for decision scopes with additional expxperience event 
AEPOfferExperienceEvent* expxperienceEvent = [[AEPOfferExperienceEvent alloc] initWithXdm:@{@"key":@"value"} data:nil datasetIdentifier:nil];

[AEPMobileOfferDecisioning prefetchOffersWithDecisionScopes:@[decisionScope] experienceEvent:expxperienceEvent];
```

**Swift**

```swift
let decisionScope = DecisionScope(activityId: "xcore:offer-activity:124e8bc413c888dd", placementId: "xcore:offer-placement:124e8a16430888db")
// prefetch with only decision scopes
OfferDecisioning.prefetchOffers(decisionScopes: [decisionScope ])

// prefetch with additional data
let experienceEvent = OfferExperienceEvent(xdm: ["xdmkey": "xdmvalue"], data: nil, datasetIdentifier: "override-datasetId")

OfferDecisioning.prefetchOffers(decisionScopes: [decisionScope ], experienceEvent: experienceEvent)
```
{% endtab %}
{% endtabs %}

## retrievePrefetchedOffers

This API retrieves the prefetched offers for the targeted decision scopes from the cache. The returned dictionary will only contains offers for decision scopes that has already been prefetched and cached. If a certain decision scope has not been prefetched before, it won't be contained in the returned dictionary.

{% tabs %}
{% tab title="Android" %}
#### Syntax

```java
public static void retrievePrefetchedOffers(final List<DecisionScope> decisionScopes, final AdobeCallbackWithError<Map<DecisionScope, List<Offer>>> callback)
```

#### Example

#### Java

```java
OfferDecisioning.retrievePrefetchedOffers(Arrays.asList(
                new DecisionScope("xcore:offer-activity:11cfb1fa93381aca", "xcore:offer-placement:1175009612b0100c")),
                new AdobeCallbackWithError<Map<DecisionScope, List<Offer>>>() {
                    @Override
                    public void fail(AdobeError adobeError) {

                    }
                    @Override
                    public void call(Map<DecisionScope, List<Offer>> decisionScopeListMap) {
                        StringBuffer sb = new StringBuffer();
                        // render the offer with offer.content
                    }
                });
```
{% endtab %}

{% tab title="iOS — Swift" %}
#### Syntax

```swift
func retrievePrefetchedOffers(decisionScopes: [DecisionScope], completionHandler: @escaping ([DecisionScope: [Offer]], Error?) -> Void)
```

* _callback_ is invoked with the `[DecisionScope: [Offer]]` type of  value. An `Error` will be returned if SDK fails to retrieve the offers.

#### Examples

Here are the examples in Objective C and Swift:

#### **Objective C**

```objectivec
AEPDecisionScope* homeDecisionScope = [[AEPDecisionScope alloc] initWithActivityId:@"xcore:offer-activity:124e8bc413c888dd" placementId:@"xcore:offer-placement:124e8a16430888db"];

[AEPMobileOfferDecisioning retrievePrefetchedOffersWithDecisionScopes:@[homeDecisionScope] completionHandler:^(NSDictionary<AEPDecisionScope *,NSArray<AEPOffer*>*>* offers, NSError * error) {
          // get the offers for homeDecisionScope
              NSArray<AEPOffer*>* homeOffers = offers[homeDecisionScope]
          // deal with the offers
}];
```

**Swift**

```swift
let homeDecisionScope = DecisionScope(activityId: "xcore:offer-activity:124e8bc413c888dd", placementId: "xcore:offer-placement:124e8a16430888db")

OfferDecisioning.retrievePrefetchedOffers(decisionScopes: [homeDecisionScope]) { offersDict, _ in

                    // get the offers for homeDecisionScope
                    if let homeOffers = offersDict[homeDecisionScope] {
                        // deal with the offers
                    }
                }
```
{% endtab %}
{% endtabs %}

## Public classes

{% tabs %}
{% tab title="Android" %}
### DecisionScope

This class encapsulates the decision `activityId`, `placementId` and `itemCount`. The `DecisionScope` object can be used to fetch offers from the Offer Decisioning service when it is enabled in the `Datastreams` on the Data collection UI. The default value for `itemCount` is 1, if not provided when creating the `DecisionScope` object.

```java
final public class DecisionScope {
    
    public DecisionScope(final String activityId, final String placementId) {...}

    public DecisionScope(final String activityId, final String placementId, final int itemCount) {...}

    public String getActivityId() {...}

    public String getPlacementId() {...}

    public int getItemCount() {...}
```

### Proposition

This class represents the proposition received from the offer decisioning service upon personalization query.

```java
public class Proposition {

    Proposition(final String id, final List<Offer> offers, final String scopeString, final DecisionScope decisionScope) {...}

    public String getId() {...}

    List<Offer> getOffers() {...}

    public String getScopeString() {...}
```

### Offer

This class represents the offer option received from the offer decisioning service upon personalization query.

```java
public class Offer {

    Offer(final String id, final String etag, final String schema, final OfferType type, final List<String> language, final String content, final Map<String, String> characteristics) {...}

    public String getId() {...}

    public String getEtag() {...}

    public OfferType getType() {...}

    public List<String> getLanguage() {...}

    public String getContent() {...}

    public Map<String, String> getCharacteristics() {...}

    public Proposition getProposition() {...}
```

### OfferType

An enum indicating the type of an offer. This is based on the offer `format` field returned in the personalization query response.

```java
public enum OfferType {
    UNKNOWN, JSON, HTML, IMAGE, TEXT {
        @Override
        public String toString() {
            return "text/plain";
        }
    };

    static OfferType from(final String type) {...}
}
```

### OfferExperienceEvent

An instance of `OfferExperienceEvent` can be supplied in the prefetch API when additional information such as xdm data, free-form data or dataset identifier needs to be passed to the Offer Decisioning service. If provided, the `datasetIdentitifer` overrides the default dataset configured in the `Datastreams` on the Data Collection UI.

```java
public class OfferExperienceEvent {
    
    public OfferExperienceEvent(final Map<String, Object> xdmData) {...}

    public OfferExperienceEvent(final Map<String, Object> xdmData, final Map<String, Object> data, final String datasetIdentifier) {...}

    public Map<String, Object> getXdmData() {...}

    public Map<String, Object> getData() {...}

    public String getDatasetIdentifier() {...}
}
```
{% endtab %}
{% tab title="iOS — Swift" %}
### DecisionScope/**AEPDecisionScope**

This class contains the id of activity and placement, which is used by the offer decisioning service to propose offers for. For advanced use case you can also assign the value of `itemCount`, if not, a default value of 1 will be used.

```swift
@objc(AEPDecisionScope)
public class DecisionScope{
    @objc public let activityId: String
    @objc public let placementId: String
    @objc public let itemCount: Int

    @objc public init(activityId: String, placementId: String, itemCount: Int = 1) {...}
}
```

### Proposition/AEPProposition

This class represents the proposition received from the offer decisioning service.

```swift
@objc(AEPProposition)
public class Proposition: NSObject, Codable {
    @objc public let id: String
    @objc public let scopeString: String
    @objc public let decisionScope: DecisionScope
    @objc public lazy var offers: [Offer] = {...}()
}
```

### Offer/AEPOffer

This class represents the offer option received from the offer decisioning service.

```swift
@objc(AEPOffer)
public class Offer: NSObject, Codable {
    @objc public let id: String
    @objc public let etag: String
    @objc public let type: OfferType
    @objc public let language: [String]?
    @objc public let content: String?
    @objc public let characteristics: [String: String]?
    @objc public weak var proposition: Proposition?
}
```

### OfferType/AEPOfferType

An enum indicating the type of an offer, which is a field of the `Offer` class

```swift
public enum OfferType{
    case unknown = 0
    case json = 1
    case text = 2
    case html = 3
    case image = 4
}
```

### OfferExperienceEvent/**AEPOfferExperienceEvent**

An instance of `OfferExperienceEvent` need to be passed to the prefetch API when additional context data need to be provided to the Offer Decisioning services.

```swift
public class OfferExperienceEvent: NSObject {
    /// XDM formatted data, use an `XDMSchema` implementation for a better XDM data injestion and format control
    @objc public let xdm: [String: Any]

    /// Optional free-form data associated with this event
    @objc public let data: [String: Any]?

    /// Adobe Experience Platform dataset identifier, if not set the default dataset identifier set in the Datastream configuration is used
    @objc public let datasetIdentifier: String?

    /// Initialize an Experience Event with the provided event data
    /// - Parameters:
    ///   - xdm:  XDM formatted data for this event, passed as a raw XDM Schema data dictionary.
    ///   - data: Any free form data in a [String : Any] dictionary structure.
    ///   - datasetIdentifier: The Experience Platform dataset identifier where this event should be sent to; if not provided, the default dataset identifier set in the Datastream configuration is used
    @objc public init(xdm: [String: Any], data: [String: Any]? = nil, datasetIdentifier: String? = nil) {...}
}
```
{% endtab %}
{% endtabs %}

