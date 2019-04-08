# Using your own monitor

You can also use your monitoring services and integrate with Places by using the Places Extension APIs.

## Registering Geofences

If you decide to use your monitoring services, register the geofences of the POIs around your current location by completing the following steps:

{% tabs %}
{% tab title="iOS" %}
1. Pass the location updates that were obtained from the Core Location services of the iOS to the Places Extension. 
2. Use the `getNearbyPointsOfInterest` Places Extension API to get the array of _n_ `ACPPlacesPoi` objects around the current location.

   ```text
   - (void) locationManager: (CLLocationManager*) manager didUpdateLocations: (NSArray<CLLocation*>*) locations {

          [ACPPlaces getNearbyPointsOfInterest:currentLocation limit:10 callback: ^ (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi) {
              [self startMonitoringGeoFences:nearbyPoi];
      }];

   }
   ```

3. Extract the information from the obtained `ACPPlacesPOI` objects and start monitoring those POIs

```text
- (void) startMonitoringGeoFences: (NSArray*) newGeoFences {
    // verify if the device supports monitoring geofences
    // check for location permission

    for (ACPPlacesPoi * currentRegion in newGeoFences) {
        // make the circular region
        CLLocationCoordinate2D center = CLLocationCoordinate2DMake(currentRegion.latitude, currentRegion.longitude);
        CLCircularRegion* currentCLRegion = [[CLCircularRegion alloc] initWithCenter:center                                                                                                                              radius:currentRegion.radius                                                                                                                    identifier:currentRegion.identifier];
        currentCLRegion.notifyOnExit = YES;
        currentCLRegion.notifyOnEntry = YES;

        // start monitoring the new region
        [_locationManager startMonitoringForRegion:currentCLRegion];

    }
}
```
{% endtab %}

{% tab title="Android" %}
1. Pass the location updates that were obtained from the Google Play services or the Android location services to the Places Extension.
2. Use the `getNearbyPointsOfInterest` Places Extension API to get the list of n `PlacesPoi` objects around the current location.

```java
    LocationCallback callback = new LocationCallback() {
            @Override
            public void onLocationResult(LocationResult locationResult) {
                super.onLocationResult(locationResult);

                Places.getNearbyPointsOfInterest(currentLocation, 10, new            AdobeCallback<List<PlacesPOI>>() {
            @Override
            public void call(List<PlacesPOI> pois)
                starMonitoringGeofence(pois);
            }
        });

            }
        };
```

1. Extract the data from the obtained `PlacesPOI` objects and start monitoring those POIs.

```java
private void startMonitoringFences(final List<PlacesPOI> nearByPOIs) {
    // check for location permission
    for (PlacesPOI poi : nearByPOIs) {
            final Geofence fence = new Geofence.Builder()
            .setRequestId(poi.getIdentifier())
            .setCircularRegion(poi.getLatitude(), poi.getLongitude(), poi.getRadius())
            .setExpirationDuration(Geofence.NEVER_EXPIRE)
            .setTransitionTypes(Geofence.GEOFENCE_TRANSITION_ENTER |
                                Geofence.GEOFENCE_TRANSITION_EXIT)
            .build();
            geofences.add(fence);
        }

        GeofencingRequest.Builder builder = new GeofencingRequest.Builder();
        builder.setInitialTrigger(GeofencingRequest.INITIAL_TRIGGER_ENTER);
        builder.addGeofences(geofences);
        builder.build();
           geofencingClient.addGeofences(builder.build(), geoFencePendingIntent)
}
```
{% endtab %}
{% endtabs %}

Calling the `getNearbyPointsOfInterest` API results in a network call that gets the location around the current location.

**Important** : You should call the API sparingly or only when there is significant location change of the user.

## Posting Geofence Events

{% tabs %}
{% tab title="iOS" %}
Call the `processGeofenceEvent` Places API in the CLLocationManager delegate. This API notifies you whether the user has entered or exited a specific region.

```objectivec
- (void) locationManager:(CLLocationManager *)manager didEnterRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeEntry];
}

- (void) locationManager:(CLLocationManager *)manager didExitRegion:(CLRegion *)region {
    [ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeExit];
}
```
{% endtab %}

{% tab title="Android" %}
Call the `processGeofenceEvent` API in your `IntentService` that is registered to receive Android geofence events.

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
{% endtabs %}

