# AEPPlaces Public APIs

This document contains usage information for the public functions, classes, and enums in AEPPlaces.

## Static Functions

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

Clears out the client-side data for Places in shared state, local storage, and in-memory.

{% tabs %}
{% tab title="Swift" %}
<b>Signature:</b>
```
static func clear()
```
<b>Example Usage:</b>
```
Places.clear()
```
{% endtab %}
{% tab title="Objective-c" %}
<b>Signature:</b>
```
+ (void) clear;
```
<b>Example Usage:</b>
```
[AEPMobilePlaces clear];
```
{% endtab %}
{% endtabs %}

<hr />

### extensionVersion

Returns the running version of the AEPPlaces extension.

{% tabs %}
{% tab title="Swift" %}
<b>Signature:</b>
```
static var extensionVersion: String
```
<b>Example Usage:</b>
```
let placesVersion = Places.extensionVersion
```
{% endtab %}
{% tab title="Objective-c" %}
<b>Signature:</b>
```
+ (nonnull NSString*) extensionVersion;
```
<b>Example Usage:</b>
```
NSString *placesVersion = [AEPMobilePlaces extensionVersion];
```
{% endtab %}
{% endtabs %}

<hr />

### getCurrentPointsOfInterest

Returns all Points of Interest (POI) of which the device is currently known to be within.

{% tabs %}
{% tab title="Swift" %}
<b>Signature:</b>
```
static func getCurrentPointsOfInterest(_ closure: @escaping ([PointOfInterest]) -> Void)
```
<b>Example Usage:</b>
```
Places.getCurrentPointsOfInterest() { currentPois in
    print("currentPois: \(currentPois)")
}
```
{% endtab %}
{% tab title="Objective-c" %}
<b>Signature:</b>
```
+ (void) getCurrentPointsOfInterest: ^(NSArray<AEPPlacesPoi*>* _Nonnull pois) closure;
```
<b>Example Usage:</b>
```
[AEPMobilePlaces getCurrentPointsOfInterest:^(NSArray<AEPPlacesPoi *> *pois) {
    NSLog(@"currentPois: %@", pois);
}];
```
{% endtab %}
{% endtabs %}

<hr />

### getLastKnownLocation

Returns the last latitude and longitude provided to the AEPPlaces Extension.

If the Places Extension does not have a valid last known location for the user, the parameter passed in the closure will be `nil`. The CLLocation object returned by this method will only ever contain valid data for latitude and longitude, and is not meant to be used for plotting course, speed, altitude, etc.

{% tabs %}
{% tab title="Swift" %}
<b>Signature:</b>
```
static func getLastKnownLocation(_ closure: @escaping (CLLocation?) -> Void)
```
<b>Example Usage:</b>
```
Places.getLastKnownLocation() { location in
    if let location = location {
        print("location returned from closure: (\(location.coordinate.latitude), \(location.coordinate.longitude))")
    }
}
```
{% endtab %}
{% tab title="Objective-c" %}
<b>Signature:</b>
```
+ (void) getLastKnownLocation: ^(CLLocation* _Nullable lastLocation) closure;
```
<b>Example Usage:</b>
```
[AEPMobilePlaces getLastKnownLocation:^(CLLocation *location) {
    if (location) {
        NSLog(@"location returned from closure: (%f, %f)", location.coordinate.latitude, location.coordinate.longitude);
    }    
}];
```
{% endtab %}
{% endtabs %}

<hr />

### getNearbyPointsOfInterest

Requests a list of nearby Points of Interest (POI) and returns them in a closure.

{% tabs %}
{% tab title="Swift" %}
<b>Signature:</b>
```
static func getNearbyPointsOfInterest(forLocation location: CLLocation,
                                      withLimit limit: UInt,
                                      closure: @escaping ([PointOfInterest], PlacesQueryResponseCode) -> Void)
```
<b>Example Usage:</b>
```
let location = CLLocation(latitude: 40.4350229, longitude: -111.8918356)
Places.getNearbyPointsOfInterest(forLocation: location, withLimit: 10) { (nearbyPois, responseCode) in    
    print("responseCode: \(responseCode.rawValue) - nearbyPois: \(nearbyPois)")
}
```
{% endtab %}
{% tab title="Objective-c" %}
<b>Signature:</b>
```
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: ^ (NSArray<AEPPlacesPoi*>* _Nonnull, AEPPlacesQueryResponseCode) closure;
```
<b>Example Usage:</b>
```
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

<hr />

### processRegionEvent

Passes a `CLRegion` and a `PlacesRegionEvent` to be processed by the Places extension.

Calling this method will result in an Event being dispatched to the SDK's EventHub. This enables rule processing based on the triggering region event.

{% tabs %}
{% tab title="Swift" %}
<b>Signature:</b>
```
static func processRegionEvent(_ regionEvent: PlacesRegionEvent,
                               forRegion region: CLRegion)
```
<b>Example Usage:</b>
```
let region = CLCircularRegion(center: CLLocationCoordinate2D(latitude: 40.3886845, longitude: -111.8284979),
                              radius: 100,
                              identifier: "877677e4-3004-46dd-a8b1-a609bd65a428")

Places.processRegionEvent(.entry, forRegion: region)
```
{% endtab %}
{% tab title="Objective-c" %}
<b>Signature:</b>
```
+ (void) processRegionEvent: (AEPRegionEventType) eventType
                  forRegion: (nonnull CLRegion*) region;
```
<b>Example Usage:</b>
```
CLCircularRegion *region = [[CLCircularRegion alloc] initWithCenter:CLLocationCoordinate2DMake(40.3886845, -111.8284979)
                                                             radius:100
                                                         identifier:@"877677e4-3004-46dd-a8b1-a609bd65a428"];

[AEPMobilePlaces processRegionEvent:AEPPlacesRegionEventEntry forRegion:region];
```
{% endtab %}
{% endtabs %}

<hr />

### registerExtension

This API no longer exists in `AEPPlaces`. Instead, the extension should be registered by calling the `registerExtensions` API in the `MobileCore`.

{% tabs %}
{% tab title="Swift" %}
<b>Example:</b>
```
MobileCore.registerExtensions([Places.self])
```
{% endtab %}
{% tab title="Objective-c" %}
<b>Example:</b>
```
[AEPMobileCore registerExtensions:@[AEPMobilePlaces.class] completion:nil];
```
{% endtab %}
{% endtabs %}

<hr />

### setAuthorizationStatus

Sets the authorization status in the Places extension.

The status provided is stored in the Places shared state, and is for reference only. Calling this method does not impact the actual location authorization status for this device.

{% hint style="important" %}
This method should only be called from the `CLLocationManagerDelegate` protocol method  [locationManagerDidChangeAuthorization(_:)](https://developer.apple.com/documentation/corelocation/cllocationmanagerdelegate/3563956-locationmanagerdidchangeauthoriz).
{% endhint %}

{% tabs %}
{% tab title="Swift" %}
<b>Signature:</b>
```
static func setAuthorizationStatus(status: CLAuthorizationStatus)
```
<b>Example Usage:</b>
```
// in the class implementing CLLocationManagerDelegate:

func locationManagerDidChangeAuthorization(_ manager: CLLocationManager) {
    Places.setAuthorizationStatus(status: manager.authorizationStatus)
}
```
{% endtab %}
{% tab title="Objective-c" %}
<b>Signature:</b>
```
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```
<b>Example Usage:</b>
```
// in the class implementing CLLocationManagerDelegate:

- (void)locationManagerDidChangeAuthorization:(CLLocationManager *)manager {
    [AEPMobilePlaces setAuthorizationStatus:manager.authorizationStatus];
}
```
{% endtab %}
{% endtabs %}

<hr />

## Additional Classes and Enums

| Type | Swift | Objective-c |
| ---- | ----- | ----------- |
| class | `PointOfInterest` | `AEPPlacesPoi` |
| enum | `PlacesQueryResponseCode` | `AEPlacesQueryResponseCode` |
| enum | `PlacesRegionEvent` | `AEPPlacesRegionEvent` |

#### PointOfInterest

| Name | Data Type |
| ---- | --------- |
| identifier | String |
| latitude | Double |
| libraryId | String |
| longitude | Double |
| metaData | [String: String] |
| name | String |
| radius | Int |
| userIsWithin | Bool |
| weight | Int |

#### PlacesQueryResponseCode

| Case | Raw Value |
| ---- | ---------
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
| ---- | --------- |
| entry | 0 |
| exit | 1 |
