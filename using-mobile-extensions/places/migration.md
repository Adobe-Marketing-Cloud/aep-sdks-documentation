# Migration from ACPPlaces \(iOS\)

This document is a reference comparison of ACPPlaces \(2.x\) APIs against their equivalent APIs in AEPPlaces \(3.x\).

If explanation beyond showing API differences is necessary, it will be captured as a "hint" within that API's section.

For example:

{% hint style="info" %}
This is information that is important to help clarify the API.
{% endhint %}

## Primary class

The class name containing public APIs is different depending on the SDK and language combination used.

| SDK Version | Language | Class Name | Example |
| :--- | :--- | :--- | :--- |
| ACPPlaces | Objective-C | `ACPPlaces` | `[ACPPlaces clear];` |
| AEPPlaces | Objective-C | `AEPMobilePlaces` | `[AEPMobilePlaces clear];` |
| AEPPlaces | Swift | `Places` | `Places.clear()` |

## Additional public classes and enums

| ACPPlaces \(Objective-C\) | AEPPlaces \(Objective-C\) | AEPPlaces \(Swift\) |
| :--- | :--- | :--- |
| `ACPPlacesRequestError` | `AEPPlacesQueryResponseCode` | `PlacesQueryResponseCode` |
| `ACPPlacesPoi` | `AEPPlacesPoi` | `PointOfInterest` |
| `ACPRegionEventType` | `AEPPlacesRegionEvent` | `PlacesRegionEvent` |

## Public APIs \(alphabetical\)

* [clear](migration.md#clear)
* [extensionVersion](migration.md#extensionVersion)
* [getCurrentPointsOfInterest](migration.md#getCurrentPointsOfInterest)
* [getLastKnownLocation](migration.md#getLastKnownLocation)
* [getNearbyPointsOfInterest](migration.md#getNearbyPointsOfInterest)
* [processRegionEvent](migration.md#processRegionEvent)
* [registerExtension](migration.md#registerExtension)
* [setAuthorizationStatus](migration.md#setAuthorizationStatus)

### clear

{% tabs %}
{% tab title="ACPPlaces \(Objective-C\)" %}
```text
+ (void) clear;
```
{% endtab %}

{% tab title="AEPPlaces \(Objective-C\)" %}
```text
+ (void) clear;
```
{% endtab %}

{% tab title="AEPPlaces \(Swift\)" %}
```swift
static func clear()
```
{% endtab %}
{% endtabs %}

### extensionVersion

{% tabs %}
{% tab title="ACPPlaces \(Objective-C\)" %}
```text
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}

{% tab title="AEPPlaces \(Objective-C\)" %}
```text
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}

{% tab title="AEPPlaces \(Swift\)" %}
```swift
static var extensionVersion: String
```
{% endtab %}
{% endtabs %}

### getCurrentPointsOfInterest

{% tabs %}
{% tab title="ACPPlaces \(Objective-C\)" %}
```text
+ (void) getCurrentPointsOfInterest: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable userWithinPoi)) callback;
```
{% endtab %}

{% tab title="AEPPlaces \(Objective-C\)" %}
```text
+ (void) getCurrentPointsOfInterest: ^(NSArray<AEPPlacesPoi*>* _Nonnull pois) closure;
```
{% endtab %}

{% tab title="AEPPlaces \(Swift\)" %}
```swift
static func getCurrentPointsOfInterest(_ closure: @escaping ([PointOfInterest]) -> Void)
```
{% endtab %}
{% endtabs %}

### getLastKnownLocation

{% tabs %}
{% tab title="ACPPlaces \(Objective-C\)" %}
{% hint style="info" %}
If the SDK has no last known location, it will pass a `CLLocation` object with a value of `999.999` for latitude and longitude to the callback.
{% endhint %}

```text
+ (void) getLastKnownLocation: (nullable void (^) (CLLocation* _Nullable lastLocation)) callback;
```
{% endtab %}

{% tab title="AEPPlaces \(Objective-C\)" %}
```text
+ (void) getLastKnownLocation: ^(CLLocation* _Nullable lastLocation) closure;
```
{% endtab %}

{% tab title="AEPPlaces \(Swift\)" %}
{% hint style="info" %}
If the SDK has no last known location, it will pass `nil` to the closure.
{% endhint %}

```swift
static func getLastKnownLocation(_ closure: @escaping (CLLocation?) -> Void)
```
{% endtab %}
{% endtabs %}

### getNearbyPointsOfInterest

{% tabs %}
{% tab title="ACPPlaces \(Objective-C\)" %}
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

{% tab title="AEPPlaces \(Objective-C\)" %}
```text
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: ^ (NSArray<AEPPlacesPoi*>* _Nonnull, AEPPlacesQueryResponseCode) closure;
```
{% endtab %}

{% tab title="AEPPlaces \(Swift\)" %}
{% hint style="info" %}
Rather than providing an overloaded method, a single method supports retrieval of nearby Points of Interest. The provided closure accepts two parameters, representing the resulting nearby points of interest \(if any\) and the response code.
{% endhint %}

```swift
static func getNearbyPointsOfInterest(forLocation location: CLLocation,
                                      withLimit limit: UInt,
                                      closure: @escaping ([PointOfInterest], PlacesQueryResponseCode) -> Void)
```
{% endtab %}
{% endtabs %}

### processRegionEvent

{% tabs %}
{% tab title="ACPPlaces \(Objective-C\)" %}
{% hint style="info" %}
The order of parameters has the `CLRegion` that triggered the event first, and the `ACPRegionEventType` second.
{% endhint %}

```text
+ (void) processRegionEvent: (nonnull CLRegion*) region
         forRegionEventType: (ACPRegionEventType) eventType;
```
{% endtab %}

{% tab title="AEPPlaces \(Objective-C\)" %}
```text
+ (void) processRegionEvent: (AEPRegionEventType) eventType
                  forRegion: (nonnull CLRegion*) region;
```
{% endtab %}

{% tab title="AEPPlaces \(Swift\)" %}
{% hint style="info" %}
The order of parameters has the `PlacesRegionEvent` first, and the `CLRegion` that triggered the event second. This aligns better with Swift API naming conventions.
{% endhint %}

```swift
static func processRegionEvent(_ regionEvent: PlacesRegionEvent,
                               forRegion region: CLRegion)
```
{% endtab %}
{% endtabs %}

### registerExtension

{% tabs %}
{% tab title="ACPPlaces \(Objective-C\)" %}
```text
+ (void) registerExtension;
```
{% endtab %}

{% tab title="AEPPlaces \(Objective-C\)" %}
{% hint style="info" %}
Registration occurs by passing `AEPMobilePlaces` to the `[AEPMobileCore registerExtensions:completion:]` API.
{% endhint %}

```text
[AEPMobileCore registerExtensions:@[AEPMobilePlaces.class] completion:nil];
```
{% endtab %}

{% tab title="AEPPlaces \(Swift\)" %}
{% hint style="info" %}
Registration occurs by passing `Places` to the `MobileCore.registerExtensions` API.
{% endhint %}

```swift
MobileCore.registerExtensions([Places.self])
```
{% endtab %}
{% endtabs %}

### setAuthorizationStatus

{% tabs %}
{% tab title="ACPPlaces \(Objective-C\)" %}
```text
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```
{% endtab %}

{% tab title="AEPPlaces \(Objective-C\)" %}
```text
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```
{% endtab %}

{% tab title="AEPPlaces \(Swift\)" %}
```swift
static func setAuthorizationStatus(status: CLAuthorizationStatus)
```
{% endtab %}
{% endtabs %}

