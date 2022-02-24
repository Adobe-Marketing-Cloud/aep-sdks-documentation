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

Clears out the client-side data for Places in shared state, local storage, and in-memory.

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

Returns the running version of the AEPPlaces extension.

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

Returns all points of interest \(POI\) of which the device is currently known to be within.

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

Returns the last latitude and longitude provided to the AEPPlaces Extension.

If the Places Extension does not have a valid last known location for the user, the parameter passed in the closure will be `nil`. The `CLLocation` object returned by this method will only contain a valid coordinate. Other properties on the `CLLocation` object should not be considered valid.

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
{% hint style="info" %}
If the SDK has no last known location, it will pass `nil` to the closure.
{% endhint %}

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

Requests a list of nearby Points of Interest \(POI\) and returns them in a closure.

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

Passes a `CLRegion` and a `PlacesRegionEvent` to be processed by the Places extension.

Calling this method will result in an `Event` being dispatched to the SDK's `EventHub`. This enables rule processing based on the triggering region event.

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

This API no longer exists in `AEPPlaces`. Instead, the extension should be registered by calling the `registerExtensions` API in the `MobileCore`.

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

Sets the authorization status in the Places extension.

The status provided is stored in the Places shared state, and is for reference only. Calling this method does not impact the actual location authorization status for this device.

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

