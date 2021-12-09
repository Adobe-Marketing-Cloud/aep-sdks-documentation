# Validation and next steps

As you begin to add solution APIs to your mobile implementation, you are going to want to validate that specific actions and experiences work as intended. Adding the [Assurance extension](../foundation-extensions/adobe-experience-platform-assurance/README.md) to your application at the beginning of your implementation provides a way to quickly check to make sure the SDK has been instrumented properly and that data is flowing to Adobe Analytics and other solutions.

Adobe Assurance, previously known as Project Griffon, is available across all [SDK platforms and frameworks](../current-sdk-versions.md). Installation and setup instructions are available [here](../foundation-extensions/adobe-experience-platform-assurance/README.md).

Once you have Assurance integrated, you can create a new session by either scanning a QR code or by following a unique deep link URL.

The main interface for Griffon will show a running event list of all SDK events, including a configuration response event that will provide a readout of all configuration values obtained from Adobe Experience Platform Launch.

![Project Griffon Configuration Response](../.gitbook/assets/configurationresponse.png)

## Adobe Analytics view

The Adobe Analytics event list offers a focused view of analytics events triggered in the application. You can sort through all of the track action and track state calls. In the Analytics view in the Assurance UI, you can see both the raw hit request sent to Analytics and the post-processed details.

![Project Griffon analytics view](../.gitbook/assets/GriffonAnalytics.png)

## Places Service view

Assurance simplifies testing point of interest entries and exits. The Places event list provides a focused view showing all events related to Places Service, including user authorization level granted and requests for nearby points of interest \(POIs\).

While a device is connected to an active Assurance session, the map view will show a timeline of POI entries and exits. If you want to test actions or experiences triggered by geofence entries and exits, the map view will allow you to spoof or simulate your location by clicking on any area within the map.

To learn more about the Places Service, please read the [Places Service overview](https://experienceleague.adobe.com/docs/places/using/home.html?lang=en)

![Project Griffon Places Service Location Simulation](../.gitbook/assets/GriffonPlaces.png)

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://experienceleague.adobe.com/?support-solution=General#support) for immediate assistance

