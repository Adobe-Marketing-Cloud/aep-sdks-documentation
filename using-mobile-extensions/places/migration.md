# Migration from ACPPlaces to AEPPlaces

This document is a reference comparison of ACPPlaces (2.x) APIs against their equivalent APIs in AEPPlaces (3.x).

If explanation beyond showing API differences is necessary, it will be captured as a "hint" within that API's section.  

For example:

{% hint style="info" %}
This is information that is important to help clarify the API.
{% endhint %}

## Primary Class

The class name containing public APIs is different depending on which SDK and language combination being used.

| SDK Version | Language | Class Name | Example |
| ----------- | -------- | ---------- | ------- |
| ACPPlaces | Objective-c | `ACPPlaces` | `[ACPPlaces clear];`|
| AEPPlaces | Objective-c | `AEPMobilePlaces` | `[AEPMobilePlaces clear];` |
| AEPPlaces | Swift | `Places` | `Places.clear()` |

## Additional Public Classes and Enums

| ACPPlaces (Objective-c) | AEPPlaces (Objective-c) | AEPPlaces (Swift) |
| ----------------------- | ----------------------- | ----------------- |
| `ACPPlacesRequestError` | `AEPPlacesQueryResponseCode` | `PlacesQueryResponseCode` |
| `ACPPlacesPoi` | `AEPPlacesPoi` | `PointOfInterest` |
| `ACPRegionEventType` | `AEPPlacesRegionEvent` | `PlacesRegionEvent` |

## Public APIs (alphabetical)
- [clear](#clear)
- [extensionVersion](#extensionVersion)
- [getCurrentPointsOfInterest](#getCurrentPointsOfInterest)
- [getLastKnownLocation](#getLastKnownLocation)
- [getNearbyPointsOfInterest](#getNearbyPointsOfInterest)
- [processRegionEvent](#processRegionEvent)
- [registerExtension](#registerExtension)
- [setAuthorizationStatus](#setAuthorizationStatus)

<hr />

### clear

{% tabs %}
{% tab title="ACPPlaces (Objective-c)" %}
```
+ (void) clear;
```
{% endtab %}
{% tab title="AEPPlaces (Objective-c)" %}
```
+ (void) clear;
```
{% endtab %}
{% tab title="AEPPlaces (Swift)" %}
```
static func clear()
```
{% endtab %}
{% endtabs %}

<hr />

### extensionVersion

{% tabs %}
{% tab title="ACPPlaces (Objective-c)" %}
```
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}
{% tab title="AEPPlaces (Objective-c)" %}
```
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}
{% tab title="AEPPlaces (Swift)" %}
```
static var extensionVersion: String
```
{% endtab %}
{% endtabs %}

<hr />

### getCurrentPointsOfInterest

{% tabs %}
{% tab title="ACPPlaces (Objective-c)" %}
```
+ (void) getCurrentPointsOfInterest: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable userWithinPoi)) callback;
```
{% endtab %}
{% tab title="AEPPlaces (Objective-c)" %}
```
+ (void) getCurrentPointsOfInterest: ^(NSArray<AEPPlacesPoi*>* _Nonnull pois) closure;
```
{% endtab %}
{% tab title="AEPPlaces (Swift)" %}
```
static func getCurrentPointsOfInterest(_ closure: @escaping ([PointOfInterest]) -> Void)
```
{% endtab %}
{% endtabs %}

<hr />

### getLastKnownLocation

{% tabs %}
{% tab title="ACPPlaces (Objective-c)" %}

{% hint style="info" %}
If the SDK has no last known location, it will pass a `CLLocation` object with a value of `999.999` for latitude and longitude to the callback.
{% endhint %}

```
+ (void) getLastKnownLocation: (nullable void (^) (CLLocation* _Nullable lastLocation)) callback;
```
{% endtab %}
{% tab title="AEPPlaces (Objective-c)" %}
```
+ (void) getLastKnownLocation: ^(CLLocation* _Nullable lastLocation) closure;
```
{% endtab %}
{% tab title="AEPPlaces (Swift)" %}

{% hint style="info" %}
If the SDK has no last known location, it will pass `nil` to the closure.
{% endhint %}

```
static func getLastKnownLocation(_ closure: @escaping (CLLocation?) -> Void)
```
{% endtab %}
{% endtabs %}

<hr />

### getNearbyPointsOfInterest

{% tabs %}
{% tab title="ACPPlaces (Objective-c)" %}

{% hint style="info" %}
Two `getNearbyPointsOfInterest` methods exist. The overloaded version allows the caller to provide an `errorCallback` parameter in the case of failure.
{% endhint %}

```
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
{% tab title="AEPPlaces (Objective-c)" %}
```
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: ^ (NSArray<AEPPlacesPoi*>* _Nonnull, AEPPlacesQueryResponseCode) closure;
```
{% endtab %}
{% tab title="AEPPlaces (Swift)" %}

{% hint style="info" %}
Rather than providing an overloaded method, a single method supports retrieval of nearby Points of Interest. The provided closure accepts two parameters, representing the resulting nearby Points of Interest (if any) and the response code.
{% endhint %}

```
static func getNearbyPointsOfInterest(forLocation location: CLLocation,
                                      withLimit limit: UInt,
                                      closure: @escaping ([PointOfInterest], PlacesQueryResponseCode) -> Void)
```
{% endtab %}
{% endtabs %}

<hr />

### processRegionEvent

{% tabs %}
{% tab title="ACPPlaces (Objective-c)" %}

{% hint style="info" %}
The order of parameters has the `CLRegion` that triggered the event first, and the `ACPRegionEventType` second.
{% endhint %}

```
+ (void) processRegionEvent: (nonnull CLRegion*) region
         forRegionEventType: (ACPRegionEventType) eventType;
```
{% endtab %}
{% tab title="AEPPlaces (Objective-c)" %}
```
+ (void) processRegionEvent: (AEPRegionEventType) eventType
                  forRegion: (nonnull CLRegion*) region;
```
{% endtab %}
{% tab title="AEPPlaces (Swift)" %}

{% hint style="info" %}
The order of parameters has the `PlacesRegionEvent` first, and the `CLRegion` that triggered the event second. This aligns better with Swift API naming conventions.
{% endhint %}

```
static func processRegionEvent(_ regionEvent: PlacesRegionEvent,
                               forRegion region: CLRegion)
```
{% endtab %}
{% endtabs %}

<hr />

### registerExtension

{% tabs %}
{% tab title="ACPPlaces (Objective-c)" %}
```
+ (void) registerExtension;
```
{% endtab %}
{% tab title="AEPPlaces (Objective-c)" %}

{% hint style="info" %}
Registration occurs by passing `AEPMobilePlaces` to the `[AEPMobileCore registerExtensions:completion:]` API.
{% endhint %}

```
[AEPMobileCore registerExtensions:@[AEPMobilePlaces.class] completion:nil];
```
{% endtab %}
{% tab title="AEPPlaces (Swift)" %}

{% hint style="info" %}
Registration occurs by passing `Places` to the `MobileCore.registerExtensions` API.
{% endhint %}

```
MobileCore.registerExtensions([Places.self])
```
{% endtab %}
{% endtabs %}

<hr />

### setAuthorizationStatus

{% tabs %}
{% tab title="ACPPlaces (Objective-c)" %}
```
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```
{% endtab %}
{% tab title="AEPPlaces (Objective-c)" %}
```
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```
{% endtab %}
{% tab title="AEPPlaces (Swift)" %}
```
static func setAuthorizationStatus(status: CLAuthorizationStatus)
```
{% endtab %}
{% endtabs %}

<hr />
