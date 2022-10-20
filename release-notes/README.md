---
description: Release notes and change logs for the Adobe Experience Platform Mobile SDKs.
---

# Release notes

{% hint style="success" %}
## Project Griffon will be Assurance!
We're pleased to announce that Project Griffon will be generally available to all Adobe Experience Cloud customers as Assurance. To learn more about this transition see [here](../../beta/project-griffon/).
{% endhint %}

## October 19, 2022

#### iOS AEPEdge 1.5.0

* Adds support for persisting the location hint returned by the Edge Network for the duration of the session for an improved user experience. Includes new APIs `getLocationHint` and `setLocationHint` allowing hybrid applications to share the location hint across SDKs.

#### Android Edge 1.4.0

* Adds support for persisting the location hint returned by the Edge Network for the duration of the session for an improved user experience. Includes new APIs `getLocationHint` and `setLocationHint` allowing hybrid applications to share the location hint across SDKs.

## October 12, 2022

### iOS AEPTarget 3.3.0

* Added support for remote property token (`at_property`) updates via Experience Platform Data Collection rules.
* Added support for raw Target APIs to fetch mbox content and to send notifications to Adobe Target.
  * The `executeRawRequest` API can be used to prefetch or execute mbox locations (even non-unique mbox locations). The API callback will be invoked with the full response data from Adobe Target if the request is successful, or with an error message otherwise.
  * The `sendRawNotifications` API can be used to send display or click notifications to Adobe Target. The event token required for these requests can be retrieved from the response of a prior prefetch or execute call via `executeRawRequest` API.

### Android Target 1.4.0

* Added support for raw Target APIs to fetch mbox content and to send notifications to Adobe Target.
  * The `executeRawRequest` API can be used to prefetch or execute mbox locations (even non-unique mbox locations). The API callback will be invoked with the full response data from Adobe Target if the request is successful, or with a null value otherwise.
  * The `sendRawNotifications` API can be used to send display or click notifications to Adobe Target. The event token required for these requests can be retrieved from the response of a prior prefetch or execute call via `executeRawRequest` API.

### Adobe Target extension 2.5.0

* Added support for a new Event Type `Raw Request` in Adobe Target extension for creating rules on the Experience Platform Data Collection UI. This can be used for handling advanced scenarios when using the raw Target APIs.

## October 10, 2022

### Android Optimize 1.0.1

* Fixed an issue where Base64 encoding the JSON string, created using the `activityId` and `placementId` provided in the `DecisionScope` constructor, introduced a newline character in the encoded scope string.

## September 9, 2022

### Android Core 1.11.4

* Fixed a bug that prevents bundled rules from being retrieved from the correct location.

## September 8, 2022

### Android Core 1.11.3

* Fixed a bug that prevents early events from being processed correctly by the rules engine.
* Removed unnecessary `AtomicBoolean` usage while listening to Android Activity lifecycle changes.

## September 1, 2022

### iOS Campaign Classic 3.0.0

* Initial release to support [Adobe Campaign Classic workflows](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/master/using-mobile-extensions/adobe-campaignclassic) for Adobe Experience Platform Mobile SDKs for iOS in Swift. This extension library is available as an [open source project on Github](https://github.com/adobe/aepsdk-campaignclassic-ios/).

## August 25, 2022

### iOS ACPCore 2.9.6

* Fix race conditions in HitQueue.

### iOS ACPAnalytics 2.5.4

* Fix race conditions in AnalyticsHitQueue to prevent crash related to concurrent reset of database.

## August 18, 2022

### Android Core 1.11.2

* Added support for bundled rules.
* Fixed a crash that can occur while extracting data from launch intent of an Android Activity.

### Android Identity 1.3.2

* Fixed a crash that can occur during construction of a query string of IDs.

## August 10, 2022

### iOS AEPCore 3.7.1

* Made improvements to retry logic when downloading the remote Configuration fails
* Made changes in Identity to speed up boot up
* Fixed a bug where early events do not properly get processed by the rules engine
* Improved Objective-C naming for MessagingDelegate methods
* Updated UI classes to respect safe area when showing fullscreen messages

## August 2, 2022

### Android Target 1.3.0

Added getter and setter APIs for Target tnt IDs and session IDs to enable cross-channel sessions.

* The `setSessionId` API should be invoked prior to any Target request to prevent the Mobile SDK from generating a session ID locally. The session ID will follow the session expiry as governed by the `target.sessionTimeout` configuration setting. You can use this API in conjunction with `setTntId` API to set both of the value in the SDK.
* The `setTntId` API, when invoked, also sets the Target edge host value in the SDK by deriving it from the profile location hint supplied in the tnt ID.
* The `getSessionId` and `getTntId` APIs can be used to retrieve the current Target session ID and tnt ID values respectively.

## July 29, 2022

### iOS AEPTarget 3.2.0

Added getter and setter APIs for Target tnt IDs and session IDs to enable cross-channel sessions.

* The `setSessionId` API should be invoked prior to any Target request to prevent the Mobile SDK from generating a session ID locally. The session ID will follow the session expiry as governed by the `target.sessionTimeout` configuration setting.You can use this API in conjunction with `setTntId` API to set both of the value in the SDK.
* The `setTntId` API, when invoked, also sets the Target edge host value in the SDK by deriving it from the profile location hint supplied in the tnt ID.
* The `getSessionId` and `getTntId` APIs can be used to retrieve the current Target session ID and tnt ID values respectively.

## July 25, 2022

### ACP React Native Core 2.0.2

* Targeting Android 12 (API 31) for the Android implementation.

### AEP React Native Core 1.0.1

* Targeting Android 12 (API 31) for the Android implementation.


## June 30, 2022

### iOS AEPAnalytics 3.2.0

* Added tvOS support.

### iOS AEPMedia 3.1.0

* Added tvOS support.

## June 16, 2022

### iOS AEPCore 3.7.0

* Added tvOS support.
* Fixed a few race conditions in the EventHub and MobileCore.
* Made changes in AEPIdentity to speed up boot.

## June 15, 2022

### Android Core 1.11.1

* Fixed a crash which was caused by an exception thrown from the Android Activity class.

## June 10, 2022

### Adobe Journey Optimizer - Decisioning extension 1.0.0

`Adobe Journey Optimizer - Decisioning` extension is now available in the extensions catalog on the Data Collection UI for mobile Tag Properties. No configuration is necessary for this extension.  

## June 9, 2022

### Android Optimize 1.0.0

The `Adobe Experience Platform Mobile SDK - Optimize` extension is now available for Android!

This extension enables real-time personalization workflows in your mobile applications when using Adobe Target and/or Adobe Journey Optimizer Offer Decisioning.

**Key Features**

With this release, the extension provides APIs that you can use to:

* Fetch personalized offers from the decisioning services enabled in the datastreams e.g. Adobe Target, Adobe Journey Optimizer Offer Decisioning.
* Track user interactions with those offers.

## June 7, 2022

### iOS AEPEdgeIdentity 1.1.0

* Added the `getUrlVariables` API to support passing the visitor ID from a mobile app to a web view.
* Added support for advertising identifier and ad tracking consent collection.

### Android EdgeIdentity 1.1.0

* Added the `getUrlVariables` API to support passing the visitor ID from a mobile app to a web view.
* Added support for advertising identifier and ad tracking consent collection.
* Internal fixes for IdentityMap deserialization.

### iOS ACPAnalytics 2.5.3

* Fix crash in AnalyticsHitDatabase caused by unprotected shared access of AnalyticsState object.

## June 2, 2022

### iOS AEPEdge 1.4.1

* Updates the consent request to use "update" query operation in order to allow for incremental consent preferences changes.
* Internal updates to use URLComponents builder for Edge endpoints.

### Android Edge 1.3.2

* Updates the consent request to use "update" query operation in order to allow for incremental consent preferences changes.
* Updates internal network stack to use Mobile Core's ServiceProvider Network Service, reducing overall extension code size.

## May 27, 2022

### iOS AEPOptimize 1.0.0

The `Adobe Experience Platform Mobile SDK - Optimize` extension is now available for iOS!

This extension enables real-time personalization workflows in your mobile applications when using Adobe Target and/or Adobe Journey Optimizer Offer Decisioning.

**Key Features**

With this release, the extension provides APIs that you can use to:

* Fetch personalized offers from the decisioning services enabled in the datastreams e.g. Adobe Target, Adobe Journey Optimizer Offer Decisioning.
* Track user interactions with those offers.

### Android Campaign Standard 1.0.9

* Fixed a compatibility issue seen when using the Campaign Standard and Messaging In-App beta extensions in the same mobile app.

## May 26, 2022

### iOS AEPTarget 3.1.3

* Fixed an issue where the Target display notification was not being sent to the server, upon invoking `displayedLocations` API, if a prior prefetch call did not return profile state token for the mbox.

## May 24, 2022

### iOS Analytics 2.5.2

* Fixed a bug for the integration with Assurance where "No Debug Flag" was showing in the UI for some events.

## May 18, 2022

### iOS AEPAudience 3.0.4

* Fixed an issue where lifecycle data was included in signalWithData requests.

### Android Campaign Classic 1.0.2

* Android Campaign Classic SDK is now Adobe Campaign Classic (ACC) v8 compatible! Broadlog ID can be provided in the UUID format in the notification tracking APIs.

## May 17, 2022

### iOS Campaign Classic 2.1.1

* ACPCampaignClassic iOS SDK is now Adobe Campaign Classic (ACC) v8 compatible! Broadlog ID can be provided in the UUID format in the notification tracking APIs.

## May 12, 2022

### iOS AEPAnalytics 3.1.0

* Added support for using the Analytics Extension in [App Extensions](https://developer.apple.com/app-extensions/)

## May 9, 2022

### iOS AEPCore 3.6.0

* Added support for using the Core SDK in [App Extensions.](https://developer.apple.com/app-extensions/)
* Added a new API to the Extension protocol for getting the latest non-pending shared state.
* Added support for using Bundled Rules.
* Added support for cached images for Fullscreen Messages.
* Fixed a bug preventing Fullscreen Messages from being dismissed in certain conditions.

### iOS AEPAudience 3.0.3

- Fixed integration with Lifecycle extension to send lifecycle metrics when a new app session is started.

## April 28, 2022

### ACP React Native plugins

Updated the following ACP React Native packages to remove the usage of deprecated Jcenter() repository:
- [@adobe/react-native-acpcore v2.0.1](https://www.npmjs.com/package/@adobe/react-native-acpcore/v/2.0.1)
- [@adobe/react-native-acpuserprofile v2.0.1](https://www.npmjs.com/package/@adobe/react-native-acpuserprofile/v/2.0.1)
- [@adobe/react-native-aepassurance v2.0.1](https://www.npmjs.com/package/@adobe/react-native-aepassurance/v/2.0.1)
- [@adobe/react-native-acpmedia v3.0.1](https://www.npmjs.com/package/@adobe/react-native-acpmedia/v/3.0.1)
- [@adobe/react-native-acptarget v2.0.1](https://www.npmjs.com/package/@adobe/react-native-acptarget/v/2.0.1)
- [@adobe/react-native-acpcampaign v2.0.1](https://www.npmjs.com/package/@adobe/react-native-acpcampaign/v/2.0.1)
- [@adobe/react-native-acpplaces v2.0.1](https://www.npmjs.com/package/@adobe/react-native-acpplaces/v/2.0.1)
- [@adobe/react-native-acpaudience v2.0.1](https://www.npmjs.com/package/@adobe/react-native-acpaudience/v/2.0.1)
- [@adobe/react-native-acpanalytics v2.0.1](https://www.npmjs.com/package/@adobe/react-native-acpanalytics/v/2.0.1)

## April 21, 2022

### Android Core 1.11.0

* Internal fixes to support In-App Messaging with the AEPMessaging extension.
* Fixed a crash that could happen while initializing event history database.

### Android Identity 1.3.1

* Improved extension stability by adding additional error checks when processing sync identifier requests.

## April 12, 2022

### AEP React Native plugins

The following AEP SDK React Native plugins have been published:

 - @adobe/react-native-aepcore@1.0.0
 - @adobe/react-native-aepuserprofile@1.0.0
 - @adobe/react-native-aepassurance@3.0.0
 - @adobe/react-native-aepedge@1.0.0
 - @adobe/react-native-aepedgeconsent@1.0.0
 - @adobe/react-native-aepedgeidentity@1.0.0

For more details, see the documentation and release notes in the [aepsdk-react-native repository](https://github.com/adobe/aepsdk-react-native).


## April 8, 2022

### iOS AEPCore 3.5.0

* Adds two APIs to `Date+Format` class. Method `getISO8601UTCDateWithMilliseconds` formats a Date to string as with fractional seconds and UTC time zone, while `getISO8601FullDate` formats a Date to string with date without time using the local time zone.
* Lifecycle foreground and background events for Edge Network now format timestamps with fractional seconds and UTC time zone.
* Updates the timestamp format for rule token `~timestampp` with fractional seconds and UTC time zone. This rule token is used to set the mobile property data element "Adobe Experience Platform Timestamp".
* Improves Signal logging by treating all 2xx network responses as success.
* Fixes bug where dispatched events failed due to use of single quotes in name.
* Fixes format of push token string by uppercasing characters.

### iOS AEPEdge 1.4.0

* Updates timestamp in Experience Events to use fractional seconds.
* Deprecates APIs `XDMFormatters.dateToISO8601String` and `XDMFormatters.dateToFullDateString`. Use the `Date` extension methods `getISO8601UTCDateWithMilliseconds` and `getISO8601FullDate` instead, provided by the AEPServices module within the AEPCore extension.

### iOS AEPEdgeConsent 1.0.1

* Updates timestamp in Consent requests to use fractional seconds.

## April 2, 2022

### iOS AEPAssurance 1.1.4

* Fixed a bug that caused Assurance to not connect to a session if your iOS app's `info.plist` contains a property of type `date`.

Note: This release pertains to Assurance mobile extension that works with ACPCore

## April 1, 2022

### iOS AEPEdgeIdentity 1.0.1

* Synchronized updates and reads on the Identity for Edge Network shared state to avoid any race conditions.

### Adobe Experience Platform Edge Network Launch extension v1.1.9

* UI updates for the Datastream configuration section to enable the sandbox aware datastreams support. If more than one sandbox is used, a sandbox picker is displayed to allow for datastreams selection across sandboxes.

* Auto-complete in the UI for default third party domain based on company name for Edge Network data collection. The domain configuration is now required, while existing configurations will continue to use the default edge.adobedc.net domain.

### Adobe Journey Optimizer Launch extension v0.0.16

* UI updates to support the new datastream selections in the AEP Edge Network extension.

## March 31, 2022

### iOS AEPAnalytics 3.0.4

* Fixed `getTrackingIdentifier` and `getVisitorIdentifier` APIs to `return nil` instead of `AEPError.unexpected` error when AID/VID values are not found in persistence.

## March 30, 2022

## End of support for Adobe Experience Platform Mobile SDK plugins for Unity

* Effective March 30, 2022, support for Adobe Experience Platform Mobile SDKs on Unity is no longer active. While you may continue using our libraries, Adobe no longer plans to update, modify, or provide support for these libraries. Please contact your Adobe CSM for details.

## March 11, 2022

### Android Core 1.10.1

* Updates the timestamp format for rule token `~timestampp`  with fractional seconds and UTC time zone. This rule token is used to set the mobile property data element "Adobe Experience Platform Timestamp".

### Android Lifecycle 1.1.1

* Lifecycle foreground and background events for Edge Network now format timestamps with fractional seconds and UTC time zone.

### Android Edge 1.3.1

* Updates timestamp in Experience Events to use fractional seconds.

### Android Consent 1.0.1

* Updates timestamp in Consent requests to use fractional seconds.

## March 4, 2022

### ACP Xamarin frameworks

Updated the Android and iOS native libraries for the [ACPCore](https://github.com/adobe/xamarin-acpcore) and [ACPAnalytics](https://github.com/adobe/xamarin-acpanalytics) Xamarin frameworks:

* [Xamarin Core Android 1.1.0](https://www.nuget.org/packages/Adobe.ACPCore.Android/1.1.0): Android Core updated to 1.10.0
* [Xamarin Identity Android 1.1.0](https://www.nuget.org/packages/Adobe.ACPIdentity.Android/1.1.0): Android Identity updated to 1.3.0
* [Xamarin Lifecycle Android 1.1.0](https://www.nuget.org/packages/Adobe.ACPLifecycle.Android/1.1.0): Android Lifecycle updated to 1.1.0
* [Xamarin Signal Android 1.0.1](https://www.nuget.org/packages/Adobe.ACPSignal.Android/1.0.1): Android Signal updated to 1.0.4
* [Xamarin Core iOS 1.0.1](https://www.nuget.org/packages/Adobe.ACPCore.iOS/1.0.1): iOS Core updated to 2.9.5
* [Xamarin Core tvOS 1.0.1](https://www.nuget.org/packages/Adobe.ACPCore.tvOS/1.0.1): tvOS Core updated to 2.9.5
* [Xamarin Analytics Android 1.0.1](https://www.nuget.org/packages/Adobe.ACPAnalytics.Android/1.0.1): Android Analytics updated to 1.2.10
* [Xamarin Analytics iOS 1.0.1](https://www.nuget.org/packages/Adobe.ACPAnalytics.iOS/1.0.1): iOS Analytics updated to 2.5.1
* [Xamarin Analytics tvOS 1.0.1](https://www.nuget.org/packages/Adobe.ACPAnalytics.tvOS/1.0.1): tvOS Analytics updated to 2.5.1

## March 3, 2022

### Android Analytics 1.2.10

* Fixed a bug for the integration with Assurance where "No Debug Flag" was showing in the UI for some events.

## February 22, 2022

### iOS Assurance 3.0.1
* Add support for transmitting large events.
* Assurance extension now prompts an error message when attempting to connect to a deleted session.
* Improved logging for troubleshooting.
* Fixed an issue to ensure that event collection stops on session disconnection.

### Android Assurance 1.0.4
* Add support for transmitting large events.
* Assurance extension now prompts an error message when attempting to connect to a deleted session.
* Improved logging for troubleshooting.
* Fixed an issue to ensure that event collection stops on session disconnection.

## February 14, 2022

### iOS Core 2.9.5
* Updates version for bundled ACPIdentity 2.5.2 release.

### iOS Identity 2.5.2
* Fixes intermittent issue for GetUrlVariables and AppendToUrl APIs when custom Analytics identifiers are being used.

## February 9, 2022

### iOS Campaign Standard 3.0.1

* Fixed an issue with the Campaign message tracking URL being incorrectly built.

## February 8, 2022

### Android Identity 1.3.0

- Added a `device_consent` status parameter when `setAdvertisingIdentifier` is called after ad tracking is enabled/disabled.
- Added support to handle the MobileCore.resetIdentities() API.
- Fixes intermittent issue for GetUrlVariables and AppendToUrl APIs when custom Analytics identifiers are being used.
- Stability improvements for network connections.

Released with sdk-core version 1.10.0

## February 7, 2022

### Android Core 1.10.0

* Added support for a new API `clearUpdatedConfiguration()`, see Configuration API reference for more details.
* Added support for optionally capturing event history on the device.
* Added support for triggering rules engine conditions based on event history.
* Added public platform support for datastore and UI services.

## February 3, 2022

### iOS AEPServices 3.4.2
* Add `@objc` attribute to `messageSettings` in `FullscreenMessage`

## January 26, 2022

### iOS AEPCore 3.4.1
* Fixed AEPRulesEngine dependency in Package.swift

### ACP Unity packages

The ACP Unity packages now use XCFrameworks in order to support hardware with the new Apple M1 architecture, while maintaining support for existing Intel architecture. See the respective GitHub repositories for the updated installation instructions.

**IMPORTANT:** Upgrading to XCFrameworks distribution requires Xcode 12.0 or newer.

Below is a list of the new versions for each Unity package:

* [Unity ACPCore v1.0.1](https://github.com/adobe/unity-acpcore/releases/tag/v1.0.1)
* [Unity ACPAnalytics v1.0.0](https://github.com/adobe/unity-acpanalytics/releases/tag/v1.0.0)
* [Unity ACPUserProfile v1.0.0](https://github.com/adobe/unity-aepassurance/releases/tag/v1.0.0)
* [Unity AEPAssurance v1.0.0](https://github.com/adobe/unity_acpuserprofile/releases/tag/v1.0.0)

## January 21, 2022

### iOS AEPEdge 1.3.0

* Allows setting a custom first-party domain that is used to interact with the mapped Adobe-provisioned Edge Network domain.

### Android AEPEdge 1.3.0

* Allows setting a custom first-party domain that is used to interact with the mapped Adobe-provisioned Edge Network domain.

## January 20, 2022

### iOS AEPCore 3.4.0
* Added support for a new API `clearUpdatedConfiguration()`, see Configuration API reference for more details.
* Added support for optionally capturing event history on the device.
* Added support for triggering rules engine conditions based on event history.

### iOS AEPServices 3.4.0
* Expanded configuration options for Fullscreen Messages.
* Added support for delegating in-app message delivery.

## January 14, 2022

### Flutter

Updated the following flutter packages to reference Android libraries from Maven Central Repository:

* [Flutter ACPCore v2.0.1](https://pub.dev/packages/flutter_acpcore/versions/2.0.1)
* [Flutter ACPUserProfile v2.0.1](https://pub.dev/packages/flutter_acpuserprofile/versions/2.0.1)
* [Flutter ACPPlaces v2.0.1](https://pub.dev/packages/flutter_acpplaces/versions/2.0.1)
* [Flutter ACPPlacesMonitor v2.0.1](https://pub.dev/packages/flutter_acpplaces_monitor/versions/2.0.1)

### Flutter Assurance 2.0.1

- Updated the package to reference the Android library from Maven Central Repository.
- Migrated to the new Android APIs based on [FlutterPlugin](https://api.flutter.dev/javadoc/io/flutter/embedding/engine/plugins/FlutterPlugin.html).
