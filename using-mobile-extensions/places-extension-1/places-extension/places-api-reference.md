# Places API reference

## Processing a region event

When a device has crossed the boundary of one of your app's pre-defined Places regions, the region and event type should be passed to the SDK for processing.

{% tabs %}
{% tab title="Android" %}
### ProcessGeofenceEvent

#### Syntax

```java
public static void processGeofenceEvent(final GeofencingEvent geofencingEvent)
```

#### Example

Call this method in your `IntentService` that is registered for receiving Android geofence events

```java
public class GeofenceTransitionsIntentService extends IntentService {

    public GeofenceTransitionsIntentService() {
        super("GeofenceTransitionsIntentService");
    }

    protected void onHandleIntent(Intent intent) {
        GeofencingEvent geofencingEvent = GeofencingEvent.fromIntent(intent);
        // Call Adobe Places API to process information
        Places.processGeofenceEvent(geofencingEvent);
    }
}
```
{% endtab %}

{% tab title="iOS" %}
### ProcessRegionEvent

#### Syntax

```objectivec
+ (void) processRegionEvent: (nonnull CLRegion*) region forRegionEventType: (ACPRegionEventType) eventType;
```

#### Example

This method should be called in the CLLocationManager delegate, which tells if the user has entered or exited a specific region.

```objectivec
- (void) locationManager:(CLLocationManager *)manager didEnterRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeEntry];
}

- (void) locationManager:(CLLocationManager *)manager didExitRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeExit];
}
```
{% endtab %}
{% endtabs %}

## Retrieve nearby points of interest

Requests a list of nearby POIs and returns them in a callback. Returns an ordered list of nearby POIs.

{% tabs %}
{% tab title="Android" %}
### GetNearbyPointsOfInterest

#### Syntax

```java
public static void getNearbyPointsOfInterest(final Location location,
    final int limit, final AdobeCallback<List<PlacesPOI>> callback);
```

#### Example

```java
Places.getNearbyPlaces(currentLocation, 10, new AdobeCallback<List<PlacesPOI>>() {
    @Override
    public void call(List<PlacesPOI> pois) {
        // do required processing with the returned nearbyPoi array
        startMonitoringPois(pois);
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### GetNearbyPointsOfInterest

#### Syntax

```objectivec
+ (void) getNearbyPointsOfInterest: (nonnull CLLocation*) currentLocation
                             limit: (NSUInteger) limit
                          callback: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi)) callback;
```

#### Example

```objectivec
[ACPPlaces getNearbyPointsOfInterest:location
                               limit:10     
                            callback:^(NSArray<ACPPlacesPoi*>* nearbyPoi) {
    // do required processing with the returned nearbyPoi array
    [self startMonitoringPois:nearbyPOI];
}];
```
{% endtab %}
{% endtabs %}

## Retrieve current device points of interest

Requests a list of POIs that the device is known to currently be within and returns them in a callback.

{% tabs %}
{% tab title="Android" %}
### GetCurrentPointsOfInterest

#### Syntax

```java
public static void getCurrentPointsOfInterest(final AdobeCallback<List<PlacesPOI>> callback);
```

#### Example

```java
Places.getCurrentPointsOfInterest(new AdobeCallback<List<PlacesPOI>>() {
    @Override
    public void call(List<PlacesPOI> pois) {
        // use the obtained POIs that the device is within
        processUserWithinPois(pois);        
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### GetCurrentPointsOfInterest

#### Syntax

```objectivec
+ (void) getCurrentPointsOfInterest: (nullable void (^) (NSArray<ACPPlacesPoi*>* _Nullable userWithinPoi)) callback;
```

#### Example

```objectivec
[ACPPlaces getCurrentPointsOfInterest:^(NSArray<ACPPlacesPoi*>* userWithinPoi) {
    // do required processing with the returned userWithinPoi array
    [self processUserWithinPois:userWithinPoi];
}];
```
{% endtab %}
{% endtabs %}

## Get the location of the device

Requests the location of the device, as previously known by the Places extension.

{% hint style="info" %}
The Places extension only knows about locations that were provided to it via calls to [GetNearbyPointsOfInterest](places-api-reference.md).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### GetLastKnownLocation

#### Syntax

```java
public static void getLastKnownLocation(final AdobeCallback<Location> callback);
```

#### Example

```java
Places.getLastKnownLocation(new AdobeCallback<Location>() {
    @Override
    public void call(Location lastLocation) {
        // do something with the last known location
        processLastKnownLocation(lastLocation);        
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### GetLastKnownLocation

#### Syntax

```objectivec
+ (void) getLastKnownLocation: (nullable void (^) (CLLocation* _Nullable lastLocation)) callback;
```

#### Example

```objectivec
[ACPPlaces getLastKnownLocation:^(CLLocation* lastLocation) {
    // do something with the last known location
    [self processLastKnownLocation:lastLocation];
}];
```
{% endtab %}
{% endtabs %}

