# Validation and next steps

As you begin to add solution APIs to your mobile implementation, you are going to want to validate that specific actions and experiences work as intended. Adding [Adobe Experience Platform Assurance](../beta/project-griffon/#what-can-project-griffon-do-for-you) to your application at the beginning of your implementation provides a way to quickly check to make sure the SDK has been instrumented properly and that data is flowing to Adobe Analytics and other solutions.

Assurance is available across all [SDK platforms and frameworks](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions). Installation and setup instructions are available [here](../beta/project-griffon/#quick-setup).

Once you have Assurance integrated, you can create a [new session](https://aep-sdks.gitbook.io/docs/beta/project-griffon/using-project-griffon#creating-sessions) by either scanning a QR code or by following a unique deep link URL.

The main interface for Assurance will show a running event list of all SDK events, including a configuration response event that will provide a readout of all configuration values obtained from Adobe Experience Platform Launch.

![Assurance Configuration Response](../.gitbook/assets/configurationresponse.png)

## Adobe Analytics view

The [Adobe Analytics](../beta/project-griffon/using-project-griffon/adobe-analytics-and-project-griffon.md#using-project-griffon-for-adobe-analytics) event list offers a focused view of analytics events triggered in the application. You can sort through all of the track action and track state calls. In the [analytics view in Adobe Experience Platform Assurance](../beta/project-griffon/using-project-griffon/adobe-analytics-and-project-griffon.md), you can see both the raw hit request sent to Analytics and the post-processed details.

![Adobe Experience Platform Assurance analytics view](../.gitbook/assets/GriffonAnalytics.png)

## Places Service view

Adobe Experience Platform Assurance simplifies testing point of interest entries and exits. The Places event list provides a focused view showing all events related to Places Service, including user authorization level granted and requests for nearby points of interest \(POIs\).

While a device is connected to an active Adobe Experience Platform Assurance session, the map view will show a timeline of POI entries and exits. If you want to test actions or experiences triggered by geofence entries and exits, the map view will allow you to spoof or simulate your location by clicking on any area within the map.

To learn more about the Places Service, please read the [Places Service overview](https://experienceleague.adobe.com/docs/places/using/home.html?lang=en)

![Assurance Places Service Location Simulation](../.gitbook/assets/GriffonPlaces.png)

To learn more about Assurance, please read the [Assurance setup guide](../beta/project-griffon/set-up-project-griffon.md)

## Next Steps

Once you have added, initialized, and validated the Experience Platform SDK for a base implementation, you can extend SDK functionality by adding in other extensions.

To get started, see the **Mobile Foundations** and **Experience Cloud** sections in the left pane.

## Get help

* Visit the SDK [community forum](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform/ct-p/adobe-experience-platform-community) to ask questions
* Contact [Adobe Experience Cloud customer care](https://experienceleague.adobe.com/?support-solution=General#support) for immediate assistance

