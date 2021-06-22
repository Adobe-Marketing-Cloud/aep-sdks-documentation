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

This class encapsulates the decision `activityId`, `placementId` and `itemCount`. The `DecisionScope` object can be used to fetch offers from the offer decisioning service if it is enabled in the Experience Edge network. The default value for `itemCount` is 1, if not provided when creating the `DecisionScope` object.

```java
final public class DecisionScope {
    final private String activityId;
    final private String placementId;
    final private int itemCount;

    public DecisionScope(final String activityId, final String placementId) {...}

    public DecisionScope(final String activityId, final String placementId, final int itemCount) {...}

    public String getActivityId() {
        return activityId;
    }

    public String getPlacementId() {
        return placementId;
    }

    public int getItemCount() {
        return this.itemCount;
    }
```

### Proposition

This class represents the proposition received from the offer decisioning service upon personalization query.

```java
public class Proposition {
    final private String id;
    final private List<Offer> offers;
    final private String scopeString;
    final private DecisionScope decisionScope;

    Proposition(final String id, final List<Offer> offers, final String scopeString, final DecisionScope decisionScope) {...}

    public String getId() {
        return id;
    }

    List<Offer> getOffers() {
        return offers;
    }

    public String getScopeString() {
        return scopeString;
    }
```

### Offer

This class represents the offer option received from the offer decisioning service upon personalization query.

```java
public class Offer {
    final private String id;
    final private String etag;
    final private String schema;
    final private OfferType type;
    final private List<String> language;
    final private String content;
    final private Map<String, String> characteristics;

    WeakReference<Proposition> propositionReference;

    Offer(final String id, final String etag, final String schema, final OfferType type, final List<String> language, final String content, final Map<String, String> characteristics) {...}

    public String getId() {
        return id;
    }

    public String getEtag() {
        return etag;
    }

    public OfferType getType() {
        return type;
    }

    public List<String> getLanguage() {
        return language;
    }

    public String getContent() {
        return content;
    }

    public Map<String, String> getCharacteristics() {
        return characteristics;
    }

    public Proposition getProposition() {
        return propositionReference.get();
    }
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

An instance of `OfferExperienceEvent` can be supplied in the prefetch API when additional information such as xdm data, free-form data or dataset identifier needs to be passed to the offer decisioning service. If provided, the `datasetIdentitifer` overrides the default dataset configured in the `Datastreams` on Adobe Experience Platform Launch.

```java
public class OfferExperienceEvent {
    private final Map<String, Object> xdmData;
    private final Map<String, Object> data;
    private final String datasetIdentifier;

    public OfferExperienceEvent(final Map<String, Object> xdmData) {
        this.xdmData = xdmData;
        this.data = new HashMap<>();
        this.datasetIdentifier = "";
    }

    public OfferExperienceEvent(final Map<String, Object> xdmData, final Map<String, Object> data, final String datasetIdentifier) {
        this.xdmData = xdmData;
        this.data = data;
        this.datasetIdentifier = datasetIdentifier;
    }

    public Map<String, Object> getXdmData() {
        return xdmData;
    }

    public Map<String, Object> getData() {
        return data;
    }

    public String getDatasetIdentifier() {
        return datasetIdentifier;
    }
}
```
{% endtab %}
{% tab title="iOS — Swift" %}
### DecisionScope/**AEPDecisionScope**

This class contains the id of activity and placement, which is used by the offer decisioning service to propose offers for. For advanced use case you can also assign the value of `itemCount`, if not, a default value of 1 will be used.

```swift
public class DecisionScope{
    public let activityId: String
    public let placementId: String
    public let itemCount: Int

    public init(activityId: String, placementId: String, itemCount: Int = 1) {
        self.activityId = activityId
        self.placementId = placementId
        self.itemCount = itemCount
    }
}
```

### Proposition/AEPProposition

This class represents the proposition received from the offer decisioning service.

```swift
public class Proposition: NSObject, Codable {
    public let id: String
    public let scopeString: String
    public let decisionScope: DecisionScope
    public lazy var offers: [Offer] = {...}()
}
```

### Offer/AEPOffer

This class represents the offer option received from the offer decisioning service.

```swift
public class Offer: NSObject, Codable {
    public let id: String
    public let type: OfferType
    public let language: [String]?
    public let content: String?
    public let characteristics: [String: String]?
    public let schema: String
    public weak var proposition: Proposition?
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

    /// Adobe Experience Platform dataset identifier, if not set the default dataset identifier set in the Edge Configuration is used
    @objc public let datasetIdentifier: String?

    /// Initialize an Experience Event with the provided event data
    /// - Parameters:
    ///   - xdm:  XDM formatted data for this event, passed as a raw XDM Schema data dictionary.
    ///   - data: Any free form data in a [String : Any] dictionary structure.
    ///   - datasetIdentifier: The Experience Platform dataset identifier where this event should be sent to; if not provided, the default dataset identifier set in the Edge configuration is used
    @objc public init(xdm: [String: Any], data: [String: Any]? = nil, datasetIdentifier: String? = nil) {
        self.xdm = xdm
        self.data = data
        self.datasetIdentifier = datasetIdentifier
    }
}
```
{% endtab %}
{% endtabs %}

