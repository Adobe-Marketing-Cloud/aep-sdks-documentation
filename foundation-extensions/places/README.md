# Adobe Experience Platform Places Service

Adobe Experience Platform Places Service provides an SDK extension which allows you to act based on the location of your users. This extension is the interface to the [Experience Platform Places Service Web Services APIs](https://experienceleague.adobe.com/docs/places/using/web-service-api/places-web-services.html?lang=en). 

The SDK extension listens for events that contain GPS coordinates and geofence region events, and dispatches new events that are processed by the Rules Engine. The SDK extension also retrieves and delivers a list of the nearest POI for the app data that retrieves from the APIs. The regions returned by the APIs are stored in cache and persistence, which allows limited offline processing.

To get started with implementing Adobe Experience Platform Places Service on your mobile app, review documentation on [Places extension](https://experienceleague.adobe.com/docs/places/using/places-ext-aep-sdks/places-extension/places-extension.html).

## Reference

* [AEPPlaces API reference](places-usage-reference.md)
* [Migration to AEPPlaces](../../resources/migrate-to-swift.md) - Migrate your current Objective-C implementation to Swift-based SDK libraries

