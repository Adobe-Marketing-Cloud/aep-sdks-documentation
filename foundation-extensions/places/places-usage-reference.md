# Places API reference

This document contains usage information for the public functions, classes, and enums in AEPPlaces.

{% hint style="info" %}
This page only contains information about the 3.x `AEPPlaces` extension for iOS.

A full API reference for the Android `Places` extension and 2.x `ACPPlaces` extension for iOS can be found [here](https://experienceleague.adobe.com/docs/places/using/places-ext-aep-sdks/places-extension/places-api-reference.html?lang=en).
{% endhint %}

## Static functions

### clear

Clears out the client-side data for Places in shared state, local storage, and in-memory.

{% tabs %}
{% tab title="Swift" %}
**Syntax**

```swift
static func clear()
```

**Example**

```swift
Places.clear()
```
{% endtab %}

{% tab title="Objective-C" %}
**Syntax**

```text
+ (void) clear;
```

**Example**

```text
[AEPMobilePlaces clear];
```
{% endtab %}

{% tab title="React Native" %}

**Syntax**

```jsx
clear();
```

**Example**

```jsx
ACPPlaces.clear();
```
{% endtab %}

{% tab title="Flutter" %}

**Syntax**

```dart
Future<void> clear();
```

**Example**

```dart
try {
  await FlutterACPPlaces.clear;
} on PlatformException {
  log("Failed to clear Places data.");
}
```
{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```jsx
 ACPPlaces.clear = function (success, error);
 ```

* _success_ is a callback containing a general success message if the clear API executed without any errors.
* _error_ is a callback containing error information if the clear API was executed with errors.

**Example**

```csharp
ACPPlaces.clear(function(response) {  
    console.log("Successfully cleared Places data.");
}, function(error){  
    console.log(error);  
});
```
{% endtab %}

{% tab title="Xamarin" %}

**iOS syntax**

```csharp
public unsafe static void Clear();
```

**iOS example**

```csharp
ACPPlaces.Clear();
```

**Android syntax**

```csharp
public unsafe static void Clear();
```

**Android example**

```csharp
ACPPlaces.Clear();
```
{% endtab %}
{% endtabs %}

### extensionVersion

Returns the running version of the AEPPlaces extension.

{% tabs %}
{% tab title="Swift" %}
**Syntax**

```swift
static var extensionVersion: String
```

**Example**

```swift
let placesVersion = Places.extensionVersion
```
{% endtab %}

{% tab title="Objective-C" %}
**Syntax**

```text
+ (nonnull NSString*) extensionVersion;
```

**Example**

```text
NSString *placesVersion = [AEPMobilePlaces extensionVersion];
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```jsx
ACPPlaces.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPPlaces version: " + version));
```
{% endtab %}

{% tab title="Flutter" %}
**Dart**

```dart
String version = await FlutterACPPlaces.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}
**Cordova**

```jsx
ACPPlaces.extensionVersion(function(version){  
    console.log(version);
}, function(error){  
    console.log(error);  
});
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

```csharp
ACPPlaces.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

### getCurrentPointsOfInterest

Returns all points of interest \(POI\) of which the device is currently known to be within.

{% tabs %}
{% tab title="Swift" %}
**Syntax**

```swift
static func getCurrentPointsOfInterest(_ closure: @escaping ([PointOfInterest]) -> Void)
```

**Example**

```swift
Places.getCurrentPointsOfInterest() { currentPois in
    print("currentPois: (currentPois)")
}
```
{% endtab %}

{% tab title="Objective-C" %}
**Syntax**

```text
+ (void) getCurrentPointsOfInterest: ^(NSArray<AEPPlacesPoi*>* _Nonnull pois) closure;
```

**Example**

```text
[AEPMobilePlaces getCurrentPointsOfInterest:^(NSArray<AEPPlacesPoi *> *pois) {
    NSLog(@"currentPois: %@", pois);
}];
```
{% endtab %}

{% tab title="React Native" %}

**Syntax**

```jsx
getCurrentPointsOfInterest(): Promise<Array<ACPPlacesPOI>>;
```

**Example**

```jsx
ACPPlaces.getCurrentPointsOfInterest().then(pois => console.log("AdobeExperienceSDK: ACPPlaces pois: " + pois));
```
{% endtab %}

{% tab title="Flutter" %}

**Syntax**

```dart
Future<String?> get currentPointsOfInterest;
```

**Example**

```dart
String pois;
try {
  pois = await FlutterACPPlaces.currentPointsOfInterest;
} on PlatformException {
  log("Failed to get the current POI's.");
}
```
{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```jsx
 ACPPlaces.getCurrentPointsOfInterest = function (success, error);
 ```

* _success_ is a callback containing the `current points of interest` if the getCurrentPointsOfInterest API executed without any errors.
* _error_ is a callback containing error information if the getCurrentPointsOfInterest API was executed with errors.

**Example**

```csharp
ACPPlaces.getCurrentPointsOfInterest(function(response){  
    console.log("Current POI's: ", response);  
}, function(error){  
    console.log(error);  
});  
```
{% endtab %}

{% tab title="Xamarin" %}

**iOS syntax**

```csharp
public unsafe static void GetCurrentPointsOfInterest(Action<NSArray<ACPPlacesPoi>> callback);
```

* _callback_ is a callback containing the `current points of interest` if the getCurrentPointsOfInterest API executed without any errors.

**iOS example**

```csharp
Action<NSArray<ACPPlacesPoi>> action = (pois) => {
  // Your code.
}
ACPPlaces.GetCurrentPointsOfInterests(action);
```

**Android syntax**

```csharp
public unsafe static void GetCurrentPointsOfInterests (IAdobeCallback callback);
```

* _callback_ is a callback containing the `current points of interest` if the getCurrentPointsOfInterest API executed without any errors.

**Android example**

```csharp
ACPPlaces.GetCurrentPointsOfInterests(new AdobeCallback());
class AdobeCallBack : Java.Lang.Object, IAdobeCallback
{
  public void Call(Object result)
  {            
    JavaList pointOfInterset = (JavaList) result;
  }
}
```
{% endtab %}
{% endtabs %}

### getLastKnownLocation

Returns the last latitude and longitude provided to the AEPPlaces Extension.

If the Places Extension does not have a valid last known location for the user, the parameter passed in the closure will be `nil`. The `CLLocation` object returned by this method will only contain a valid coordinate. Other properties on the `CLLocation` object should not be considered valid.

{% tabs %}
{% tab title="Swift" %}
**Syntax**

```swift
static func getLastKnownLocation(_ closure: @escaping (CLLocation?) -> Void)
```

**Example**

```swift
Places.getLastKnownLocation() { location in
    if let location = location {
        print("location returned from closure: ((location.coordinate.latitude), (location.coordinate.longitude))")
    }
}
```
{% endtab %}

{% tab title="Objective-C" %}
**Syntax**

```text
+ (void) getLastKnownLocation: ^(CLLocation* _Nullable lastLocation) closure;
```

**Example**

```text
[AEPMobilePlaces getLastKnownLocation:^(CLLocation *location) {
    if (location) {
        NSLog(@"location returned from closure: (%f, %f)", location.coordinate.latitude, location.coordinate.longitude);
    }    
}];
```
{% endtab %}

{% tab title="React Native" %}

**Syntax**

```jsx
getLastKnownLocation() : Promise<?ACPPlacesLocation>;
```

**Example**

```jsx
ACPPlaces.getLastKnownLocation().then(location => console.log("AdobeExperienceSDK: ACPPlaces location: " + location));
```
{% endtab %}

{% tab title="Flutter" %}

**Syntax**

```dart
Future<String?> get lastKnownLocation;
```

**Example**

```dart
String location;
try {
  location = await FlutterACPPlaces.lastKnownLocation;
} on PlatformException {
  log("Failed to get the last known location.");
}
```
{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```jsx
ACPPlaces.getLastKnownLocation = function (success, error);
 ```

* _success_ is a callback containing the `last known location` if the getLastKnownLocation API executed without any errors.
* _error_ is a callback containing error information if the getLastKnownLocation API was executed with errors.

**Example**

```csharp
ACPPlaces.getLastKnownLocation(function(response) {  
    console.log("Last known location: ", response);
}, function(error){  
    console.log(error);  
});
```
{% endtab %}

{% tab title="Xamarin" %}

**iOS syntax**

```csharp
public unsafe static void GetLastKnownLocation(Action<CLLocation> callback);
```

* _callback_ is a callback containing the `last known location` if the GetLastKnownLocation API executed without any errors.

**iOS example**

```csharp
Action<CLLocation> action = (location) => {
  // Your code.
}
ACPPlaces.GetLastKnownLocation(action);
```

**Android syntax**

```csharp
public unsafe static void GetLastKnownLocation (IAdobeCallback callback);
```

* _callback_ is a callback containing the `last known location` if the GetLastKnownLocation API executed without any errors.

**Android example**

```csharp
ACPPlaces.GetLastKnownLocation(new AdobeCallback());
class AdobeCallBack : Java.Lang.Object, IAdobeCallback
{
  public void Call(Object result)
  {            
    Location location = (Location) object;
  }
}

```
{% endtab %}
{% endtabs %}

### getNearbyPointsOfInterest

Requests a list of nearby Points of Interest \(POI\) and returns them in a closure.

{% tabs %}
{% tab title="Swift" %}
**Syntax**

```swift
static func getNearbyPointsOfInterest(forLocation location: CLLocation,
                                      withLimit limit: UInt,
                                      closure: @escaping ([PointOfInterest], PlacesQueryResponseCode) -> Void)
```

**Example**

```swift
let location = CLLocation(latitude: 40.4350229, longitude: -111.8918356)
Places.getNearbyPointsOfInterest(forLocation: location, withLimit: 10) { (nearbyPois, responseCode) in    
    print("responseCode: (responseCode.rawValue) - nearbyPois: (nearbyPois)")
}
```
{% endtab %}

{% tab title="Objective-C" %}
**Syntax**

```text
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: ^ (NSArray<AEPPlacesPoi*>* _Nonnull, AEPPlacesQueryResponseCode) closure;
```

**Example**

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

{% tab title="React Native" %}

**Syntax**

```jsx
getNearbyPointsOfInterest(location: ACPPlacesLocation, limit: number): Promise<Array<ACPPlacesPOI>>;
```

**Example**

```jsx
let location = new ACPPlacesLocation(<latitude>, <longitude>, <optional altitude>, <optional speed>, <optional accuracy>);
ACPPlaces.getNearbyPointsOfInterest(location, <limit>).then(pois => console.log("AdobeExperienceSDK: ACPPlaces pois: " + pois)).catch(error => console.log("AdobeExperienceSDK: ACPPlaces error: " + error));
```
{% endtab %}

{% tab title="Flutter" %}

**Syntax**

```dart
Future<String?> getNearbyPointsOfInterest(
    final Map location,
    final int limit,
);
```

**Example**

```dart
String pois;
try {
  var location = {'latitude':37.3309422, 'longitude': -121.8939077};
  pois = await FlutterACPPlaces.getNearbyPointsOfInterest(location, 100);
} on PlatformException {
  log("Failed to get the nearby POI's.");
}
```
{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```jsx
ACPPlaces.getNearbyPointsOfInterest = function (location, limit, success, error);
```

* _success_ is a callback containing the `nearby points of interest` if the getNearbyPointsOfInterest API executed without any errors.
* _error_ is a callback containing error information if the getNearbyPointsOfInterest API was executed with errors.

**Example**

```csharp
var location = {latitude:37.3309422, longitude:-121.8939077};
var limit = 10; // max number of POI's to return
ACPPlaces.getNearbyPointsOfInterest(location, limit, function(response){  
    console.log("Nearby POI's: ", response);  
}, function(error){  
    console.log(error);  
});
```
{% endtab %}

{% tab title="Xamarin" %}

**iOS syntax**

```csharp
public unsafe static void GetNearbyPointsOfInterest (CLLocation currentLocation, nuint limit, Action<NSArray<ACPPlacesPoi>>? callback);
```

* _callback_ is a callback containing the `nearest points of interest` if the GetNearbyPointsOfInterest API executed without any errors.

**iOS example**

```csharp
CLLocationCoordinate2D coordinate = new CLLocationCoordinate2D();
coordinate.Latitude = 37.3309;
coordinate.Longitude = -121.8939;
int count = 10; //Nearby 10 point of interest.
Action<NSArray<ACPPlacesPoi>> action = (pois) => {
  // Your code.
}
  
ACPPlaces.GetNearbyPointsOfInterest(coordinate, count, action);
```

**Android syntax**

```csharp
public unsafe static void GetNearbyPointsOfInterest (Location location, int limit, IAdobeCallback callback);
```

* _callback_ is a callback containing the `nearest points of interest` if the GetNearbyPointsOfInterest API executed without any errors.

**Android example**

```csharp
Location location = new Location("ACPPlacesTestApp.Xamarin");
//San Jose down town coordinates.
location.Latitude = 37.3309;
location.Longitude = -121.8939;
int count = 10; //Nearby 10 point of interest.
ACPPlaces.GetNearbyPointsOfInterest(location, 10, new AdobeCallback());
class AdobeCallBack : Java.Lang.Object, IAdobeCallback
{
  public void Call(Object result)
  {            
      JavaList pointOfInterset = (JavaList) result;
  }
}
```
{% endtab %}
{% endtabs %}

### processRegionEvent

Passes a `CLRegion` and a `PlacesRegionEvent` to be processed by the Places extension.

Calling this method will result in an `Event` being dispatched to the SDK's `EventHub`. This enables rule processing based on the triggering region event.

{% tabs %}
{% tab title="Swift" %}
**Syntax**

```swift
static func processRegionEvent(_ regionEvent: PlacesRegionEvent,
                               forRegion region: CLRegion)
```

**Example**

```swift
let region = CLCircularRegion(center: CLLocationCoordinate2D(latitude: 40.3886845, longitude: -111.8284979),
                              radius: 100,
                              identifier: "877677e4-3004-46dd-a8b1-a609bd65a428")

Places.processRegionEvent(.entry, forRegion: region)
```
{% endtab %}

{% tab title="Objective-C" %}
**Syntax**

```text
+ (void) processRegionEvent: (AEPRegionEventType) eventType
                  forRegion: (nonnull CLRegion*) region;
```

**Example**

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
{% tab %}
{% tab title="Swift" %}
{% endtab %}

{% tab %}
**Syntax**
{% endtab %}

{% tab %}
```swift
static func setAccuracyAuthorization(_ accuracy: CLAccuracyAuthorization)
```
{% endtab %}

{% tab %}
**Example**
{% endtab %}

{% tab %}
```swift
Places.setAccuracyAuthorization(.fullAccuracy)
```
{% endtab %}

{% tab %}
{% tab title="Objective-C" %}
{% endtab %}

{% tab %}
**Syntax**
{% endtab %}

{% tab %}
```text
+ (void) setAccuracyAuthorization: (CLAccuracyAuthorization) accuracy;
```
{% endtab %}

{% tab %}
**Example**
{% endtab %}

{% tab %}
```text
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
**Syntax**

```swift
static func setAuthorizationStatus(status: CLAuthorizationStatus)
```

**Example**

```swift
// in the class implementing CLLocationManagerDelegate:

func locationManagerDidChangeAuthorization(_ manager: CLLocationManager) {
    Places.setAuthorizationStatus(status: manager.authorizationStatus)
}
```
{% endtab %}

{% tab title="Objective-C" %}
**Syntax**

```text
+ (void) setAuthorizationStatus: (CLAuthorizationStatus) status;
```

**Example**

```text
// in the class implementing CLLocationManagerDelegate:

- (void)locationManagerDidChangeAuthorization:(CLLocationManager *)manager {
    [AEPMobilePlaces setAuthorizationStatus:manager.authorizationStatus];
}
```
{% endtab %}

{% tab title="React Native" %}

**Syntax**

```jsx
setAuthorizationStatus(authStatus : string);
```

**Example**

```jsx
ACPPlaces.setAuthorizationStatus(ACPPlacesAuthStatus.ALWAYS);
```
{% endtab %}

{% tab title="Flutter" %}

**Syntax**

```dart
Future<void> setAuthorizationStatus(
          final ACPPlacesAuthorizationStatus status);
```

**Example**

```dart
FlutterACPPlaces.setAuthorizationStatus(ACPPlacesAuthorizationStatus.ALWAYS);
```
{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```jsx
ACPPlaces.setAuthorizationStatus = function (status, success, error);
```

* _status_ is the new value for authorizaton status.
* _success_ is a callback containing a general success message if the setAuthorizationStatus API executed without any errors.
* _error_ is a callback containing error information if the setAuthorizationStatus API was executed with errors.

**Example**

```csharp
ACPPlaces.setAuthorizationStatus(ACPPlaces.AuthorizationStatusAlways, function(response) {  
    console.log("Successfully set the authorization status.");
}, function(error){  
    console.log(error);  
});
```
{% endtab %}

{% tab title="Xamarin" %}

**iOS syntax**

```csharp
public static void SetAuthorizationStatus (CLAuthorizationStatus status);
```

**iOS example**

```csharp
ACPPlaces.SetAuthorizationStatus(CLAuthorizationStatus.Authorized);
```

**Android syntax**

```csharp
public unsafe static void SetAuthorizationStatus (PlacesAuthorizationStatus status);
```

**Android example**

```csharp
ACPPlaces.SetAuthorizationStatus(PlacesAuthorizationStatus.always);
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
