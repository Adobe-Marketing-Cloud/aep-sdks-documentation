# Migration to AEPPlaces

This document is a reference comparison of AEPPlaces \(3.x\) APIs against their equivalent ACPPlaces \(2.x\) APIs.

The AEPPlaces extension is implemented purely in Swift and is compatible with the AEPCore swift SDK. To ensure a smooth transition from the ACPPlaces SDK, there are no major changes on the API names or definition. For more details, follow the migration guide below for your Swift or Objective-C mobile application.  If explanation beyond showing API differences is necessary, it will be captured as an info hint within that API's section.

## Swift

### Public classes

| Type                   | AEP (3.x)               | ACP (2.x)             |
| ---------------------- | :---------------------- | :-------------------- |
| Primary Class (Module) | Places                  | ACPPlaces             |
| Enum                   | PlacesQueryResponseCode | ACPPlacesRequestError |
| Class                  | PointOfInterest         | AEPPlacesPoi          |
| Enum                   | PlacesRegionEvent       | AEPPlacesRegionEvent  |

### API usages

{% tabs %}
{% tab title="AEP (3.x)" %}

**clear**

```swift
Places.clear()
```

**extensionVersion**

```swift
Places.extensionVersion
```

**getCurrentPointsOfInterest**

```swift
Places.getCurrentPointsOfInterest(_ closure: @escaping ([PointOfInterest]) -> Void)
```

**getLastKnownLocation**
{% hint style="info" %}
If the SDK has no last known location, it will pass `nil` to the closure.
{% endhint %}

```swift
Places.getLastKnownLocation { (location: CLLocation?) in
  // code
}
```

**getNearbyPointsOfInterest**
{% hint style="info" %}
Rather than providing an overloaded method, a single method supports retrieval of nearby Points of Interest. The provided closure accepts two parameters, representing the resulting nearby points of interest \(if any\) and the response code.
{% endhint %}

```swift
Places.getNearbyPointsOfInterest(forLocation: location, withLimit: 10) { 
  (pointsOfInterest: [PointOfInterest], responseCode: PlacesQueryResponseCode) in
	// code
}
```

**processRegionEvent**
{% hint style="info" %}
The order of parameters has the `PlacesRegionEvent` first, and the `CLRegion` that triggered the event second. This aligns better with Swift API naming conventions.
{% endhint %}

```swift
Places.processRegionEvent(PlacesRegionEvent.entry, forRegion: region)
```

**registerExtension**
{% hint style="info" %}
Registration occurs by passing `Places` to the `MobileCore.registerExtensions` API in addition to the other extensions registered.
{% endhint %}

```swift
MobileCore.registerExtensions([..., Places.self])
```

**setAuthorizationStatus**

```swift
Places.setAuthorizationStatus(authorizationStatus)
```

{% endtab %}

{% tab title="ACP (2.x)" %}

**clear**

```swift
ACPPlaces.clear()
```

**extensionVersion**

```swift
ACPPlaces.extensionVersion()
```

**getCurrentPointsOfInterest**

```swift
ACPPlaces.getCurrentPoints { (pointsOfInterest: [ACPPlacesPoi]?) in
	// code
}
```

**getLastKnownLocation**

```swift
ACPPlaces.getLastKnownLocation { (location: CLLocation?) in
	// code
}
```

**getNearbyPointsOfInterest**

```swift
ACPPlaces.getNearbyPoints(ofInterest: location, limit: 10) { (pointsOfInterest: [ACPPlacesPoi]?) in
	// code - handle POIs
}
            
ACPPlaces.getNearbyPoints(ofInterest: location, limit: 10) { (pointsOfInterest: [ACPPlacesPoi]?) in
	// code - handle POIs
} errorCallback: { (placesRequestError: ACPPlacesRequestError) in
	// code - handle error
}
```

**processRegionEvent**

```swift
ACPPlaces.processRegionEvent(region, for: ACPRegionEventType.entry)
```

**registerExtension**

```swift
ACPPlaces.registerExtension()
```

**setAuthorizationStatus**

```swift
ACPPlaces.setAuthorizationStatus(authorizationStatus)
```

{% endtab %}
{% endtabs %}



## Objective-C

### Public classes

| Type          | AEP (3.x)                  | ACP (2.x)             |
| ------------- | :------------------------- | :-------------------- |
| Primary Class | AEPMobilePlaces            | ACPPlaces             |
| Enum          | AEPPlacesQueryResponseCode | ACPPlacesRequestError |
| Class         | AEPPlacesPoi               | ACPPlacesPoi          |
| Enum          | AEPPlacesRegionEvent       | ACPRegionEventType    |

### API usages

{% tabs %}
{% tab title="AEP (3.x)" %}

**clear**

```objective-c
[AEPMobilePlaces clear];
```

**extensionVersion**

```objective-c
[AEPMobilePlaces extensionVersion];
```

**getCurrentPointsOfInterest**

```objective-c
[AEPMobilePlaces getCurrentPointsOfInterest:^(NSArray<AEPPlacesPoi *> * _Nonnull userWithinPoi) {
	// code
}];
```

**getLastKnownLocation**
{% hint style="info" %}
If the SDK has no last known location, it will pass `nil` to the closure.
{% endhint %}

```objective-C
[AEPMobilePlaces getLastKnownLocation:^(CLLocation * _Nullable location) {
	// code
}];
```

**getNearbyPointsOfInterest**

{% hint style="info" %}
The order of parameters has the `PlacesRegionEvent` first, and the `CLRegion` that triggered the event second.
{% endhint %}

```objective-C
[AEPMobilePlaces getNearbyPointsOfInterest:location limit:10 callback:^(NSArray<AEPPlacesPoi *> * _Nonnull pointsOfInterest, enum AEPPlacesQueryResponseCode responseCode) {
	// code
}];
```

**processRegionEvent**
{% hint style="info" %}
The order of parameters has the `PlacesRegionEvent` first, and the `CLRegion` that triggered the event second. This aligns better with Swift API naming conventions.
{% endhint %}

```objective-c
[AEPMobilePlaces processRegionEvent:AEPPlacesRegionEventEntry forRegion:region];
```

**registerExtension**
{% hint style="info" %}
Registration occurs by passing `AEPMobilePlaces.class` to the `AEPMobileCore registerExtensions` API in addition to the other extensions registered.
{% endhint %}

```objective-c
[AEPMobileCore registerExtensions:@[..., AEPMobilePlaces.class] completion:^{
	// registration complete
}];
```

**setAuthorizationStatus**

```objective-c
[AEPMobilePlaces setAuthorizationStatus:authorizationStatus];
```

{% endtab %}

{% tab title="ACP (2.x)" %}

**clear**

```objective-c
[ACPPlaces clear];
```

**extensionVersion**

```objective-c
[ACPPlaces extensionVersion];
```

**getCurrentPointsOfInterest**

```objective-c
[ACPPlaces getCurrentPointsOfInterest:^(NSArray<ACPPlacesPoi *> * _Nullable userWithinPoi) {
	// code
}];
```

**getLastKnownLocation**

{% hint style="info" %}
If the SDK has no last known location, it will pass a `CLLocation` object with a value of `999.999` for latitude and longitude to the callback.
{% endhint %}

```objective-c
[ACPPlaces getLastKnownLocation:^(CLLocation * _Nullable lastLocation) {
	// code
}];
```

**getNearbyPointsOfInterest**

{% hint style="info" %}
Two `getNearbyPointsOfInterest` methods exist. The overloaded version allows the caller to provide an `errorCallback` parameter in the case of failure.
{% endhint %}

```objective-c
[ACPPlaces getNearbyPointsOfInterest:location limit:10 callback:^(NSArray<ACPPlacesPoi*> * _Nullable nearbyPoi) {
	// code - handle POIs
}];
    
[ACPPlaces getNearbyPointsOfInterest:location limit:10 callback:^(NSArray<ACPPlacesPoi*> * _Nullable nearbyPoi) {
	// code - handle POIs
} errorCallback:^(ACPPlacesRequestError result) {
	// code - handle error
}];
```

**processRegionEvent**

```objective-c
[ACPPlaces processRegionEvent:region forRegionEventType:ACPRegionEventTypeEntry];
```

**registerExtension**

```objective-c
[ACPPlaces registerExtension];
```

**setAuthorizationStatus**

```objective-c
[ACPPlaces setAuthorizationStatus:authorizationStatus];
```

{% endtab %}
{% endtabs %}