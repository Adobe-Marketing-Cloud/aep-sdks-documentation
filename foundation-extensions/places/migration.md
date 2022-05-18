# Migrating to AEPPlaces reference

This document is a reference comparison of AEPPlaces \(3.x\) APIs agains against their equivalent ACPPlaces \(2.x\) APIs.

The AEPPlaces extension is implemented purely in Swift and is compatible with the AEPCore swift SDK. To ensure a smooth transition from the ACPPlaces SDK, there are no major changes on the API names or definition. For more details, follow the migration guide below for your Swift or Objective-C mobile application. If explanation beyond showing API differences is necessary, it will be captured as an info hint within that API's section.

## Public classes

| Type | AEP 3.x \(Swift\) | AEP 3.x \(Objective-C\) | ACP 2.x \(Objective-C\) |
| :--- | :--- | :--- | :--- |
| Primary Class | Places | AEPMobilePlaces | ACPPlaces |
| Enum | PlacesQueryResponseCode | AEPPlacesQueryResponseCode | ACPPlacesRequestError |
| Class | PointOfInterest | AEPPlacesPoi | ACPPlacesPoi |
| Enum | PlacesRegionEvent | AEPPlacesRegionEvent | ACPRegionEventType |

## Public APIs \(alphabetical\)

### clear

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func clear()
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) clear;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) clear;
```
{% endtab %}
{% endtabs %}

### extensionVersion

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static var extensionVersion: String
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}
{% endtabs %}

### getCurrentPointsOfInterest

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func getCurrentPointsOfInterest(_ closure: @escaping ([PointOfInterest]) -> Void)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) getCurrentPointsOfInterest: ^(NSArray<AEPPlacesPoi*>* _Nonnull pois) closure;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) getCurrentPointsOfInterest: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable userWithinPoi)) callback;
```
{% endtab %}
{% endtabs %}

### getLastKnownLocation

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func getLastKnownLocation(_ closure: @escaping (CLLocation?) -> Void)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) getLastKnownLocation: ^(CLLocation* _Nullable lastLocation) closure;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
{% hint style="info" %}
If the SDK has no last known location, it will pass a `CLLocation` object with a value of `999.999` for latitude and longitude to the callback.
{% endhint %}

```text
+ (void) getLastKnownLocation: (nullable void (^) (CLLocation* _Nullable lastLocation)) callback;
```
{% endtab %}
{% endtabs %}

### getNearbyPointsOfInterest

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
{% hint style="info" %}
Rather than providing an overloaded method, a single method supports retrieval of nearby Points of Interest. The provided closure accepts two parameters, representing the resulting nearby points of interest \(if any\) and the response code.
{% endhint %}

```swift
static func getNearbyPointsOfInterest(forLocation location: CLLocation,
                                      withLimit limit: UInt,
                                      closure: @escaping ([PointOfInterest], PlacesQueryResponseCode) -> Void)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: ^ (NSArray<AEPPlacesPoi*>* _Nonnull, AEPPlacesQueryResponseCode) closure;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
{% hint style="info" %}
Two `getNearbyPointsOfInterest` methods exist. The overloaded version allows the caller to provide an `errorCallback` parameter in the case of failure.
{% endhint %}

```text
// without error handling
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi)) callback;

// with error handling
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi)) callback
                     errorCallback: (nullable void (^) (ACPPlacesRequestError result)) errorCallback;
```
{% endtab %}
{% endtabs %}

### processRegionEvent

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
{% hint style="info" %}
The order of parameters has the `PlacesRegionEvent` first, and the `CLRegion` that triggered the event second. This aligns better with Swift API naming conventions.
{% endhint %}

```swift
static func processRegionEvent(_ regionEvent: PlacesRegionEvent,
                               forRegion region: CLRegion)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) processRegionEvent: (AEPRegionEventType) eventType
                  forRegion: (nonnull CLRegion*) region;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
{% hint style="info" %}
The order of parameters has the `CLRegion` that triggered the event first, and the `ACPRegionEventType` second.
{% endhint %}

```text
+ (void) processRegionEvent: (nonnull CLRegion*) region
         forRegionEventType: (ACPRegionEventType) eventType;
```
{% endtab %}
{% endtabs %}

### registerExtension

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
{% hint style="info" %}
Registration occurs by passing `Places` to the `MobileCore.registerExtensions` API.
{% endhint %}

```swift
MobileCore.registerExtensions([Places.self])
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
{% hint style="info" %}
Registration occurs by passing `AEPMobilePlaces` to the `[AEPMobileCore registerExtensions:completion:]` API.
{% endhint %}

```text
[AEPMobileCore registerExtensions:@[AEPMobilePlaces.class] completion:nil];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) registerExtension;
```
{% endtab %}
{% endtabs %}

### setAuthorizationStatus

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func setAuthorizationStatus(status: CLAuthorizationStatus)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
For additional details see also [Places API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/places/places-usage-reference).
{% endhint %}

