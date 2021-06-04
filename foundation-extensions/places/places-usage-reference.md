# Places API Reference

This document contains usage information for the public functions, classes, and enums in AEPPlaces.

## Static functions

* [clear](places-usage-reference.md#clear)
* [extensionVersion](places-usage-reference.md#extensionVersion)
* [getCurrentPointsOfInterest](places-usage-reference.md#getCurrentPointsOfInterest)
* [getLastKnownLocation](places-usage-reference.md#getLastKnownLocation)
* [getNearbyPointsOfInterest](places-usage-reference.md#getNearbyPointsOfInterest)
* [processRegionEvent](places-usage-reference.md#processRegionEvent)
* [registerExtension](places-usage-reference.md#registerExtension)
* [setAccuracyAuthorization](places-usage-reference.md#setAccuracyAuthorization)
* [setAuthorizationStatus](places-usage-reference.md#setAuthorizationStatus)

### clear

Clears out the client-side data for Places in shared state, local storage, and in-memory.

{% tabs %}
{% tab title="Swift" %}
**Signature**

```swift
static func clear()
```

**Example usage**

```swift
Places.clear()
```
{% endtab %}

{% tab title="Objective-C" %}
**Signature**

```text
+ (void) clear;
```

**Example usage**

```text
[AEPMobilePlaces clear];
```
{% endtab %}
{% endtabs %}

### extensionVersion

Returns the running version of the AEPPlaces extension.

{% tabs %}
{% tab title="Swift" %}
**Signature**

```swift
static var extensionVersion: String
```

**Example usage**

```swift
let placesVersion = Places.extensionVersion
```
{% endtab %}

{% tab title="Objective-C" %}
**Signature**

```text
+ (nonnull NSString*) extensionVersion;
```

**Example usage**

```text
NSString *placesVersion = [AEPMobilePlaces extensionVersion];
```
{% endtab %}
{% endtabs %}

### getCurrentPointsOfInterest

Returns all points of interest \(POI\) of which the device is currently known to be within.

{% tabs %}
{% tab title="Swift" %}
**Signature**

```swift
static func getCurrentPointsOfInterest(_ closure: @escaping ([PointOfInterest]) -> Void)
```

**Example usage**

```swift
Places.getCurrentPointsOfInterest() { currentPois in
    print("currentPois: \(currentPois)")
}
```
{% endtab %}

{% tab title="Objective-C" %}
**Signature**

```text
+ (void) getCurrentPointsOfInterest: ^(NSArray<AEPPlacesPoi*>* _Nonnull pois) closure;
```

**Example usage**

```text
[AEPMobilePlaces getCurrentPointsOfInterest:^(NSArray<AEPPlacesPoi *> *pois) {
    NSLog(@"currentPois: %@", pois);
}];
```
{% endtab %}
{% endtabs %}

### getLastKnownLocation

Returns the last latitude and longitude provided to the AEPPlaces Extension.

If the Places Extension does not have a valid last known location for the user, the parameter passed in the closure will be `nil`. The `CLLocation` object returned by this method will only contain a valid coordinate. Other properties on the `CLLocation` object should not be considered valid.

{% tabs %}
{% tab title="Swift" %}
**Signature**

```swift
static func getLastKnownLocation(_ closure: @escaping (CLLocation?) -> Void)
```

**Example usage**

```swift
Places.getLastKnownLocation() { location in
    if let location = location {
        print("location returned from closure: (\(location.coordinate.latitude), \(location.coordinate.longitude))")
    }
}
```
{% endtab %}

{% tab title="Objective-C" %}
**Signature**

```text
+ (void) getLastKnownLocation: ^(CLLocation* _Nullable lastLocation) closure;
```

**Example usage**

```text
[AEPMobilePlaces getLastKnownLocation:^(CLLocation *location) {
    if (location) {
        NSLog(@"location returned from closure: (%f, %f)", location.coordinate.latitude, location.coordinate.longitude);
    }    
}];
```
{% endtab %}
{% endtabs %}

### getNearbyPointsOfInterest

Requests a list of nearby Points of Interest \(POI\) and returns them in a closure.

{% tabs %}
{% tab title="Swift" %}
**Signature**

```swift
static func getNearbyPointsOfInterest(forLocation location: CLLocation,
                                      withLimit limit: UInt,
                                      closure: @escaping ([PointOfInterest], PlacesQueryResponseCode) -> Void)
```

**Example usage**

```swift
let location = CLLocation(latitude: 40.4350229, longitude: -111.8918356)
Places.getNearbyPointsOfInterest(forLocation: location, withLimit: 10) { (nearbyPois, responseCode) in    
    print("responseCode: \(responseCode.rawValue) - nearbyPois: \(nearbyPois)")
}
```
{% endtab %}

{% tab title="Objective-C" %}
**Signature**

```text
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: ^ (NSArray<AEPPlacesPoi*>* _Nonnull, AEPPlacesQueryResponseCode) closure;
```

**Example usage**

```text
CLLocation *location = [[CLLocation alloc] initWithLatitude:40.4350229 longitude:-111.8918356];

[AEPMobilePlaces getNearbyPointsOfInterest:location
                                     limit:10
                                  callback:^(NSArray<AEPPlacesPoi *> *pois, AEPPlacesQueryResponseCode responseCode) {
    NSLog(@"responseCode: %ld", (long)responseCode);
    NSLog(@"nearbyPois: %@", pois);
}];
```
{% endtab %}
{% endtabs %}

### processRegionEvent

Passes a `CLRegion` and a `PlacesRegionEvent` to be processed by the Places extension.

Calling this method will result in an `Event` being dispatched to the SDK's `EventHub`. This enables rule processing based on the triggering region event.

{% tabs %}
{% tab title="Swift" %}
**Signature**

```swift
static func processRegionEvent(_ regionEvent: PlacesRegionEvent,
                               forRegion region: CLRegion)
```

**Example usage**

```swift
let region = CLCircularRegion(center: CLLocationCoordinate2D(latitude: 40.3886845, longitude: -111.8284979),
                              radius: 100,
                              identifier: "877677e4-3004-46dd-a8b1-a609bd65a428")

Places.processRegionEvent(.entry, forRegion: region)
```
{% endtab %}

{% tab title="Objective-C" %}
**Signature**

```text
+ (void) processRegionEvent: (AEPRegionEventType) eventType
                  forRegion: (nonnull CLRegion*) region;
```

**Example usage**

```text
CLCircularRegion *region = [[CLCircularRegion alloc] initWithCenter:CLLocationCoordinate2DMake(40.3886845, -111.8284979)
                                                             radius:100
                                                         identifier:@"877677e4-3004-46dd-a8b1-a609bd65a428"];

[AEPMobilePlaces processRegionEvent:AEPPlacesRegionEventEntry forRegion:region];
```
{% endtab %}
{% endtabs %}

### registerExtension

This API no longer exists in `AEPPlaces`. Instead, the extension should be registered by calling the `registerExtensions` API in the `MobileCore`.

{% tabs %}
{% tab title="Swift" %}
**Example:**

```swift
MobileCore.registerExtensions([Places.self])
```
{% endtab %}

{% tab title="Objective-C" %}
**Example:**

```text
[AEPMobileCore registerExtensions:@[AEPMobilePlaces.class] completion:nil];
```
{% endtab %}
{% endtabs %}

### setAccuracyAuthorization

Sets the accuracy authorization status in the Places extension.

The value provided is stored in the Places shared state, and is for reference only. Calling this method does not impact the actual location accuracy authorization for this device.

{% tabs %}

{% tab title="Swift"}

**Signature**

```swift
static func setAccuracyAuthorization(_ accuracy: CLAccuracyAuthorization)
```

**Example Usage**

```swift
Places.setAccuracyAuthorization(.fullAccuracy)
```
{% endtab %}

{% tab title="Objective-C"}

**Signature**

```objc
+ (void) setAccuracyAuthorization: (CLAccuracyAuthorization) accuracy;
```

**Example Usage**

```objc
[AEPMobilePlaces setAccuracyAuthorization:CLAccuracyAuthorizationFullAccuracy];
```

{% endtab %}

{% endtabs %}

### setAuthorizationStatus

Sets the authorization status in the Places extension.

The status provided is stored in the Places shared state, and is for reference only. Calling this method does not impact the actual location authorization status for this device.

{% hint style="info" %}
This method should only be called from the `CLLocationManagerDelegate` protocol method [locationManagerDidChangeAuthorization\(\_:\)](https://developer.apple.com/documentation/corelocation/cllocationmanagerdelegate/3563956-locationmanagerdidchangeauthoriz).
{% endhint %}

{% tabs %}
{% tab title="Swift" %}
**Signature**

```swift
static func setAuthorizationStatus(status: CLAuthorizationStatus)
```

**Example usage**

```swift
// in the class implementing CLLocationManagerDelegate:

func locationManagerDidChangeAuthorization(_ manager: CLLocationManager) {
    Places.setAuthorizationStatus(status: manager.authorizationStatus)
}
```
{% endtab %}

{% tab title="Objective-C" %}
**Signature**

```text
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```

**Example usage**

```text
// in the class implementing CLLocationManagerDelegate:

- (void)locationManagerDidChangeAuthorization:(CLLocationManager *)manager {
    [AEPMobilePlaces setAuthorizationStatus:manager.authorizationStatus];
}
```
{% endtab %}
{% endtabs %}

## Additional classes and enums

| Type | Swift | Objective-C |
| :--- | :--- | :--- |
| class | `PointOfInterest` | `AEPPlacesPoi` |
| enum | `PlacesQueryResponseCode` | `AEPlacesQueryResponseCode` |
| enum | `PlacesRegionEvent` | `AEPPlacesRegionEvent` |

#### PointOfInterest

| Name | Data Type |
| :--- | :--- |
| identifier | String |
| latitude | Double |
| libraryId | String |
| longitude | Double |
| metaData | \[String: String\] |
| name | String |
| radius | Int |
| userIsWithin | Bool |
| weight | Int |

#### PlacesQueryResponseCode

| Case | Raw Value |
| :--- | :--- |
| ok | 0 |
| connectivityError | 1 |
| serverResponseError | 2 |
| invalidLatLongError | 3 |
| configurationError | 4 |
| queryServiceUnavailable | 5 |
| privacyOptedOut | 6 |
| unknownError | 7 |

#### PlacesRegionEvent

| Case | Raw Value |
| :--- | :--- |
| entry | 0 |
| exit | 1 |
