# Using your own monitor

You can also use your own monitoring services and intergrate with Places using the Places Extension API's

## Registering Geofences

In the occasion of using your own monitoring services, register the geofences of the near by point of intrests around the current location by implementing the following steps.

{% tabs %}

{% tab title="iOS" %}

1. The location updates obtained from the Core Location services of the iOS should be passed to the Places Extension. Use the `getNearbyPointsOfInterest` Places Extension API to get the array of n  `ACPPlacesPoi` objects around the current location.

```objective-c
- (void) locationManager: (CLLocationManager*) manager didUpdateLocations: (NSArray<CLLocation*>*) locations {

        [ACPPlaces getNearbyPointsOfInterest:currentLocation limit:10 callback: ^ (NSArray<ACPPlacesPoi*>* _Nullable nearbyPoi) {
            [self startMonitoringGeoFences:nearbyPoi];
    }];

}
```

2. Extract the information from the obtained `ACPPlacesPOI` objects and start monitoring those POI's

```objective-c
- (void) startMonitoringGeoFences: (NSArray*) newGeoFences {
	// verify if the device supports monitoring geofences
	// check for location permission

    for (ACPPlacesPoi * currentRegion in newGeoFences) {
        // make the circular region
        CLLocationCoordinate2D center = CLLocationCoordinate2DMake(currentRegion.latitude, currentRegion.longitude);
        CLCircularRegion* currentCLRegion = [[CLCircularRegion alloc] initWithCenter:center                                                                              												radius:currentRegion.radius                                                                     											   identifier:currentRegion.identifier];
        currentCLRegion.notifyOnExit = YES;
        currentCLRegion.notifyOnEntry = YES;

        // start monitoring the new region
        [_locationManager startMonitoringForRegion:currentCLRegion];

    }
}
```



{% endtab %}

{% tab title="Android" %}

-  The location updates obtained from the google play services or the android location services should be passed to the Places Extension. Use the `getNearbyPointsOfInterest` Places Extension API to get the list of n  `PlacesPoi` objects around the current location.

  ```java
  	LocationCallback callback = new LocationCallback() {
  			@Override
  			public void onLocationResult(LocationResult locationResult) {
  				super.onLocationResult(locationResult);
                  
                  Places.getNearbyPointsOfInterest(currentLocation, 10, new 		   AdobeCallback<List<PlacesPOI>>() {
  			@Override
  			public void call(List<PlacesPOI> pois) {
  				starMonitoringGeofence(pois);
  			}
  		});
  
  			}
  		};
  ```

- Extract the data from the obtained `PlacesPOI` objects and start monitoring those points of intrests.

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

**Important** : Calling the ``getNearbyPointsOfInterest` Places Extension API, results in a network call of getting the location around the current location. Please call the API sparingly or only upon a significant location change of the user.

## Posting Geofence Events

{% tabs %}

{% tab title="iOS" %}

Call the `processGeofenceEvent` Places Extension API in the CLLocationManager delegate, which tells if the user has entered or exited a specific region

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

Call the `processGeofenceEvent`  Places Extension API in your `IntentService` that is registered for receiving Android geofence events

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