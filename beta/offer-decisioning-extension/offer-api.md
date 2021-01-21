# Offer Decisioning API Reference

## onOfferUpdate

Use this API to register a callback, it will be invoked whenever the AEP Offer Decisioning extension receives an offer response from backend services. The Offer Decisioning requests can be triggered by the `OfferDecisioning.prefetchOffers()` API, `Edge.sendEvent()` API or consequence rules.

{% tabs %}
{% tab title="iOS" %}
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
{% tab title="iOS" %}
#### Syntax

```swift
func prefetchOffers(decisionScopes: [DecisionScope])
```

#### Examples

Here are some examples in Objective C and Swift:

**Objective C**

```objectivec
AEPDecisionScope* decisionScope = [[AEPDecisionScope alloc] initWithActivityId:@"xcore:offer-activity:124e8bc413c888dd" placementId:@"xcore:offer-placement:124e8a16430888db"];

[AEPMobileOfferDecisioning prefetchOffersWithDecisionScopes:@[decisionScope]];
```

**Swift**

```swift
let decisionScope = DecisionScope(activityId: "xcore:offer-activity:124e8bc413c888dd", placementId: "xcore:offer-placement:124e8a16430888db")

OfferDecisioning.prefetchOffers(decisionScopes: [decisionScope ])
```
{% endtab %}
{% endtabs %}

## retrievePrefetchedOffers

This API retrieves the prefetched offers for the targeted decision scopes from the cache. The returned dictionary will only contains offers for decision scopes that has already been prefetched and cached. If a certain decision scope has not been prefetched before, it won't be contained in the returned dictionary.

{% tabs %}
{% tab title="iOS" %}
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
{% tab title="iOS" %}
### DecisionScope/**AEPDecisionScope**

This class contains the id of activity and placement, which is used by the offer decisioning service to propose offers for.

```swift
public class DecisionScope{
    public let activityId: String
    public let placementId: String

    public init(activityId: String, placementId: String) {
        self.activityId = activityId
        self.placementId = placementId
    }
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
{% endtab %}
{% endtabs %}

