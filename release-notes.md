---
description: Release notes and change logs for the Adobe Experience Platform Mobile SDKs.
---

# Release notes

## We want to help!

Please take a moment to fill out a [short survey](https://www.surveymonkey.com/r/AEPDocs) on how we can better assist you with enabling Adobe Experience Cloud solutions and services on your mobile apps.

## April 7, 2020

The following updates were made in this release:

### Android Griffon 1.1.4

* Fixed a bug where Griffon pinpad screen may disappear behind an activity.
* Griffon SDK attempts to seemlessly reconnect to its session on network interruption.
* Fixed a bug that prevented to establish Griffon connection on Android API 27 and below.
* Added a new Plugin interface method that gets called on Griffon session termination.

## April 2, 2020

The following updates were made in this release:

### iOS Core 2.6.0

* Added support for overriding internal network stack with customer-provided implementation. For more information, see [Override network stack](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/platform-services#ios).

## March 30, 2020

### iOS UserProfile 2.1.0

* Added an API `removeUserAttributes` to remove multiple attributes.
* Added an API `getUserAttributes` to get user attributes with provided keys.

### Android UserProfile 1.1.0

* Added an API `removeUserAttributes` to remove multiple attributes.
* Added an API `getUserAttributes` to get user attributes with provided keys.

## March 19, 2020

The following updates were made in this release:

### Android Campaign Classic 1.0.1

* Report extension details to Mobile Core for improved logging and Griffon support.
* Fixed a security issue where hex conversion method was vulnerable to hash collisions.

## March 18, 2020

The following updates were made in this release:

### iOS Campaign Classic 2.0.3

* Report extension details to Mobile Core for improved logging and Griffon support.
* Fixed an issue where passing nil callback in `registerDevice` API caused a crash.

## March 16, 2020

The following updates were made in this release:

### iOS Core 2.5.1

* Fixed a crash which happened in `ADBJsonType::Get`.
* Fixed a crash which happened in `EventHubInner::CreateOrUpdateSharedStateCommon`, the crash was introduced on the version 2.5.0.
* Fixed an internal issue where the SDK failed to create a Json array if it contains empty items.
* Improved log messages.

### iOS Identity 2.2.1

* Fixed an issue where all Identity APIs with callbacks were subject to a timeout. Only Identity APIs which use a completionHandler callback are subject to a timeout.
* Improved existing log messages and added additional logging to assist with debugging.

### iOS Signal 2.0.4

* Report extension details to Mobile Core for improved logging and Griffon support.
* Improved log messages.

### iOS Lifecycle 2.0.4

* Report extension details to Mobile Core for improved logging and Griffon support.
* Improved log messages.

## March 11, 2020

The following updates were made in this release:

### Android Target 1.1.5

* Report extension details to Mobile Core for improved logging and Griffon support.
* Target Session Id will now be added as a context data parameter `a.target.sessionId` in the internal Analytics for Target hit sent to Adobe Analytics.
* Fixed an issue, where on app close and relaunch, previously persisted tntId was not being sent in Target requests. 

## March 10, 2020

The following updates were made in this release:

### iOS Target 2.1.6

* Report extension details to Mobile Core for improved logging and Griffon support.
* Target Session Id will now be added as a context data parameter `a.target.sessionId` in the internal Analytics for Target hit sent to Adobe Analytics.

## March 2, 2020

The following updates were made in this release:

### iOS Analytics 2.2.3

* `AnalyticsResponse` events are now always dispatched regardless if the debugApi is enabled or if AAM forwarding is enabled.
* Report extension details to ACPCore for improved logging and Griffon support.
* Improved existing log messages and added additional logging to assist with debugging.

### iOS Griffon 1.1.0

* Added support for capturing device screenshot.
* Added support for forwarding application logs to Griffon.
* Added support for editing loaded launch configuration through Griffon.
* Added support for dispatching fake events from Griffon.
* Unique clientID and sessionID are now shared through Griffon shared state.
* Shared state contents of all the registered extensions are now forwarded to Griffon
* Griffon event now includes eventNumber and timestamp.
* Added an API to create ACPGriffonEvent with vendor, type, payload, and timestamp.
* Bug fixes.

### Android Griffon 1.1.3

* Added support for capturing device screenshot.
* Added support for forwarding application logs to Griffon.
* Added support for editing loaded launch configuration through Griffon.
* Added support for dispatching fake events from Griffon.
* Unique clientID and sessionID are now shared through Griffon shared state.
* Shared state contents of all the registered extensions are now forwarded to Griffon.
* Added constructors to create GriffonEvent with vendor, type, payload, and timestamp.
* Bug fixes.

## February 27, 2020

The following updates were made in this release:

### Android Core 1.5.1

* Fixed a bug where AppID used non-arabic numbers as app versions.
* Fixed a bug where app version was not included in AppID on Android 9 or above devices.
* Added Wrapper Type for Flutter.

### Android Signal 1.0.3

* Logging improvement
* Report extension details to Mobile Core for improved logging and Griffon support.

### Android Lifecycle 1.0.3

* Logging improvement
* Report extension details to Mobile Core for improved logging and Griffon support.

## February 19, 2020

The following updates were made in this release:

### iOS Core 2.5.0

* Mobile Core now shares the list of enabled extensions and their meta data through shared state.
* Added Wrapper Type for Flutter.
* Exposed eventNumber and eventTimestamp in ACPExtensionEvent class.
* Added the following API to support the completion handler with an nullable `NSError` object:
  * `getPrivacyStatusWithCompletionHandler`
  * `getSdkIdentitiesWithCompletionHandler`

### iOS Identity 2.2.0

* Report extension details to Mobile Core for improved logging and Griffon support.
* Added the following APIs to support the completionHandler callback that is available in iOS ACPCore version 2.5.0:

  * `appendToURL:withCompletionHandler`
  * `getUrlVariablesWithCompletionHandler`
  * `getIdentifiersWithCompletionHandler`
  * `getExperienceCloudIdWithCompletionHandler`

  When the `completionHandler` is used, and you are retrieving the Mobile SDK values, the timeout value is 500ms; if the operation times out or is not successful, an `NSError` is returned.

## February 13, 2020

The following updates were made in this release:

### Android Analytics 1.2.4

* Fixed an issue which, was causing some hits to be delayed.
* Fixed an issue where `AnalyticsResponse` events were not being dispatched even when the debug API was enabled.
* Report extension details to Mobile Core for improved logging and Griffon support.
* Improved existing log messages and added additional logging to assist with debugging.

## February 4, 2020

The following updates were made in this release:

### Android Core 1.5.0

* Fixed a cursor leak.
* Mobile Core now shares the list of enabled extensions and their meta data through shared state.
* Fixed an issue where the advertising identifier was duplicated in the response to the `MobileCore.getSDKIdentifiers` API.
* Added support for overriding internal network stack with customer-provided code.
* Added a new interface with failure callback, `AdobeCallbackWithError`, which can be used with the `MobileCore.getPrivacyStatus` and `MobileCore.getSdkIdentities` methods.

  We plan to gradually add the ability to enable failure callback to the other extensions.

### Android Identity 1.2.0

* Added support for the optional `AdobeCallbackWithError` callback that is available in Android Core version 1.5.0 on the following APIs:

  * `appendVisitorInfoForURL`
  * `getUrlVariables`
  * `getIdentifiers`
  * `getExperienceCloudId`

  When the `AdobeCallbackWithError` is used, and you are retrieving the Mobile SDK values, the timeout value is 500ms; if the operation times out or is not successful, an `AdobeError` is returned.

Released with sdk-core version 1.5.0.

### Android Mobile Services 1.1.1

* Improved existing log messages and added additional logging to assist with debugging.

## January 29, 2020

The following updates were made in this release:

**Android Target 1.1.4 and iOS Target 2.1.5**

* Improved existing log messages and added additional logging to assist with debugging.

**Android Campaign 1.0.3 and iOS Campaign 1.0.5**

* Improved existing log messages and added additional logging to assist with debugging.

## January 28, 2019

The following updates were made in this release:

**iOS Griffon 1.0.4**

* Griffon SDK adds and reports uniqueIdentifier and timestamp associated with eventHub events. \(works from Core v2.4.0\).
* Improved Logging to assist with debugging.

**Android Griffon 1.1.2**

* Fixed the nomenclature for the unique event identifier.

## January 27, 2020

The following updates were made in this release:

**iOS Core 2.4.0**

* Added a new property, `eventUniqueIdentifier`, to the `ACPExtensionEvent` class.
* Fixed an issue where the advertising identifier was duplicated in the response to the `getSDKIdentifiers` API.
* Fixed an issue where the SDK was trying to download the rules multiple times immediately after app launch.
* Fixed a crash on `std::__1::system_error: mutex lock failed: Invalid argument`.
* Fixed a bug where the iOS fullscreen message was unable to load cached images.

## January 25, 2020

The following updates were made in this release:

**Android Analytics 1.2.3 and iOS Analytics 2.2.2**

* `requestEventIdentifier` is now appended to all non-track events so that Lifecycle \(or other extension events that are sent to Analytics\) can be viewed with rich detail in Project Griffon.

## January 24, 2020

The following updates were made in this release:

**Android Griffon 1.1.1**

* The Griffon SDK now reports an event's source, type, sequence number and timestamp for every event.
* The Griffon SDK adds and reports `uniqueIdentifier` associated with eventHub events. This update is effective from Mobile Core version 1.4.2
* Removed unwanted resource files that were creating compilation error.
* Improved logging to assist with debugging.

## January 23, 2020

The following updates were made in this release:

**iOS Mobile Services 1.0.5**

* The shared state of the Profile extension can now be used as the traits for In-App Messaging.

**Android Mobile Services 1.1.0**

* The shared state of the Profile extension can now be used as the traits for In-App Messaging.
* Added a new API, `MobileServices.processGooglePlayInstallReferrerUrl(final String url)`, to support Google Play Install Referrer APIs.

  For more information about the Install Referrer APIs, see [Still Using InstallBroadcast? Switch to the Play Referrer API by March 1, 2020](https://android-developers.googleblog.com/2019/11/still-using-installbroadcast-switch-to.html).

## January 13, 2020

The following updates were made in this release:

**iOS Griffon 1.0.3**

* The Griffon bridge and the Griffon SDK are now unified.

  The set up steps are now slightly different. For more information, see [Set up Project Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon/set-up-project-griffon).

* The Adobe Analytics debug flag is now enabled when you start a Griffon session and is disabled when you end the session.
* The client-side Griffon UI now logs Location Service entry and exit events.
* This version is compatible with iOS 13.
* Fixed a crash in LIBDISPATCH.

**Android Griffon 1.1.0**

* The Griffon bridge and the Griffon SDK are now unified.

  The set up steps are now slightly different. For more information, see [Set up Project Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon/set-up-project-griffon).

* The Adobe Analytics debug flag is now enabled when you start a Griffon session and is disabled when you end the session.
* The client-side Griffon UI now logs Location Service entry and exit events.
* Modified the client UI to include client-side logging capabilities.
* Fixed an issue for Android API version 28 or later where multiple WebViews cannot share the same data directory.
* Added generic exception handling for exceptions that can occur when WebViews are accessed while OS is updating Chrome.

The Project Griffon web UI now has new views specifically for users who are trying to inspect and improve Adobe Analytics and Location Service \(Places\) implementations.

**Adobe Analytics View**

The new Adobe Analytics view shows you events that are only related to your Adobe Analytics implementation. The list view now displays the action/state name and event, `status`, with a newly formatted detail view. `status` tells you when an SDK event is generated \(processed\), whether the SDK has made a network request with Adobe Analytics \(queued\), and whether post-processing information about the event \(validated\) is returned. This information helps you determine whether your context data is being appropriately mapped in Adobe Analytics.

The detailed view for an Analytics track event contains the following parts:

* The originating SDK Analytics request event.
* The OOTB meta and context data from the request, such as the report suite ID, the SDK extension versions, the OOTB context data, and so on.
* The post-processed information on the Analytics event, which contains mapping of revars, evars, props, and so on.

For more information, see [Adobe Analytics and Project Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon/using-project-griffon/adobe-analytics-and-project-griffon).

**Location Service \(Places\) View**

The new Location Services views allow you to inspect location entry and exit events on the Project Griffon web UI and on a mobile device. Depending on your business workflows, these views provide a convenient interface to view location-specific data points for inspection on the web/client for in-context debugging.

For more information, see [Location Service and Project Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon/using-project-griffon/location-service-and-project-griffon).

## November 15, 2019

The following updates were made in this release:

**iOS Identity 2.1.3\(Released with ACPCore version 2.3.6 on Cocoapods\)**

* Synced custom and advertising identifiers with nil or empty values are now cleared from Identity shared state and local storage. They are also not synced with the Experience Cloud ID \(ECID\) Service.
* Fixed a threading issue where the Experience Cloud ID \(ECID\) Service response was handled on an incorrect thread potentially causing a memory corruption crash.

These changes were released as part of ACPCore CocoaPod v2.3.6.

## November 8, 2019

The following update was made in this release:

**iOS Mobile Servies 1.0.4**

* Fixed a bug where the iOS fullscreen message was unable to load cached images.

## October 30, 2019

The following updates were made in this release:

**Android Campaign 1.0.2**

* Fixed a bug where full-screen message interaction tracking was not working when a message was dismissed.
* Added support for local notification message metrics \(impression, open, and click\).
* Added support for message frequency rules \(show once and until clicked\) for local notification messages.

**iOS Campaign 1.0.4**

* Added support for local notification message metrics \(impression, open, and click\).
* Added support for message frequency rules \(show once and until clicked\) for local notification messages.

## October 28, 2019

The following change was made in this release:

**iOS and Android Campaign Standard 1.1.0**

* In the Launch extension, added the ability to reset the `pkey`.

**iOS Analytics 2.2.1**

* Analytics response content events now contain two new fields:

  * `hitHost`
  * `hitUrl`

  These fields contain the host and URL of the of the hit responsible for dispatching the response event.

**Android Analytics 1.2.2**

* Analytics response content events now contain two new fields:

  * `hitHost`
  * `hitUrl`

  These fields contain the host and URL of the of the hit responsible for dispatching the response event.

## October 25, 2019

The following updates were made in this release:

**iOS Core 2.3.5**

* Added support for the attach data rules consequence.
* Added support for a boolean-type comparison for the `Exist` or `Not Exist` rules condition.

**Android Core 1.4.5 \(Released with sdk-core version 1.4.6 on Maven\)**

* Added support for attach data rules consequence.
* Added support for a boolean-type comparison for the `Exist` or `Not Exist` rules condition.
* Fixed a bug where the `Exist` and `Not Exist` rules condition might not work for a `List` or `Map` type value.
* Fixed a bug that, when fetching the remote config from Launch, might cause a crash on some Android devices.
* Fixed a bug that, when the data URL of an activity did not contain valid schema, might cause a crash.

**Android Identity 1.1.2**

* Fixed a bug where the default Experience Cloud Server hostname is now used when no value is configured in the SDK.
* Fixed a bug where multiple custom identifiers with same `idType` value were synced with the Visitor ID Service.
* Custom visitor identifiers can now be cleared from the SDK by providing a null/empty identifier value for a previously synced `idType`.

## October 10, 2019

The following updates were made in this release:

**iOS Campaign Classic 2.0.1**

* Fixed an issue where, on iOS 13, the push token was not being extracted correctly from NSData during device registration.    
* Fixed an issue where the charset information was not being sent in the Content-Type header during device registration call.

## October 7, 2019

The following updates were made in this release:

**iOS Mobile Services 1.0.3**

* Full-screen messages now use `WKWebViews` from the `WebKit.framework`.
* Local notifications now use the `UserNotifications` framework.
* Fixed a crash that might happen when the **Click-Through** or the **Cancel** button in the Full-screen message was clicked more than once.

**Android Analytics 1.2.1**

* Fixed a bug where, on start up, the Analytics database was being modified by multiple threads.

## October 4, 2019

The following updates were made in this release:

**iOS Core 2.3.4**

* Fixed a crash that might have happened during app shutdown..    
* Fixed a bug where, when the SDK is being used in multiple threads, the SDK might not function under a race condition..    
* Fixed a bug where the downloaded rules zip file might not be decompressed.    
* Fixed a bug where the `getSdkIdentities` API used wrong key names for the Push ID and IDFA.    
* Removed the usage of UIWebView.    
* Extension listeners with null/empty type or source is now invalid and will not be registered.    

**iOS Identity 2.1.2**

* Fixed an issue where the push identifier is not contained in the Identity shared state on bootup.    
* Fixed an issue where `appendToUrl` uses the incorrect query delimiter when the source URL contains a question mark in its fragment identifier component.

## October 2, 2019

The following updates were made in this release:

**iOS Target 2.1.4**

* The Target session ID and Edge Host will now be persisted in NSUserDefaults. If there is no activity for the configured `target.sessionTimeout`, these variables will be reset. The default session timeout value is 30 minutes.    

**Android Target 1.1.3**

* The Target session ID and Edge Host will now be persisted in Shared Preferences. If there is no activity for the configured `target.sessionTimeout`, these variables will be reset. The default session timeout value is 30 minutes.    
* Fixed an issue where the null `at_property` key, which was passed in mbox parameters, was being sent in Target requests.

## September 24, 2019

The following updates were made in this release:

**iOS Audience 2.0.1**

* The `global.ssl` configuration settings are ignored, and SSL is enabled by default.
* Appends IMS OrgID to AAM demdex calls if subdomain endpoint is missing.

## September 17, 2019

The following updates were made in this release:

**Android Core 1.4.4 \(Released with sdk-core version 1.4.5 on Maven\)**

* Starting in API level 16, notifications now support `BigTextStyle`.

  This enables long notifications to be displayed without being truncated.

* Fixed the locale string in the HTTP User-Agent to follow the BCP 47 specification.

## September 10, 2019

The following updates were made in this release:

**Android Analytics 1.2.0**

* Added the following new pieces of data when reporting a crash:
  * `previousosversion`
  * `previousappid`.
* Added support for the Griffon debug API.
* The `global.ssl` configuration settings are ignored, and SSL is enabled by default.

## September 9, 2019

The following updates were made in this release:

**Android Identity 1.1.1 \(Released with sdk-core version 1.4.4 on Maven\)**

* Custom identifiers with null or empty IDs are ignored when calling the `syncIdentifier` or `syncIdentifiers` APIs because the Visitor ID Service does not support these identifiers.
* The `syncIdentifiers` API call is ignored when there is an empty Map.
* The duplicate advertising identifier value is removed from the Identity-shared state when `MobileCore.setAdvertisingIdentifier` is called with a new value.
* The `global.ssl` configuration settings are ignored, and SSL is enabled by default.
* Fixed an issue where `appendVisitorInfoForURL` uses the wrong query delimiter when the source URL contains a question mark in its fragment identifier component.

**iOS Analytics 2.2.0**

* Added support for Griffon debug API.
* The `global.ssl` configuration settings are ignored, and SSL is enabled by default.

**Android Griffon Bridge 1.0.3**

* You can use the Android Griffon Bridge version 1.0.3 with the Android Griffon SDK version 1.0.0.

**Android Griffon SDK 1.0.0**

* Starting in version 1.0.3, there is a new Artifact split from the Android Griffon Bridge.

## Aug 30, 2019

The following updates were made in this release:

**iOS Mobile Services 2.0.2**

* Added the ability to trigger an In-App message that is based on Analytics rules consequences..

**Android Mobile Services 1.0.1**

* Added the ability to trigger an In-App message that is based on Analytics rules consequences..

## Aug 20, 2019

The following updates were made in this release:

**iOS Core release 2.3.3**

* Reduced the number of threads that were being consumed by the SDK and also reduced the CPU usage of the SDK.
* Fixed a memory leak issue.
* Several minor fixes for the Local Notification.

**iOS Identity release 2.1.1**

* Fixed a bug where the push identifier was not updated in the Identity-shared state when `setPushIdentifier` was called.

**iOS Lifecycle release 2.0.3**

* Fixed a bug in the App ID string where `CFBundleVersion` and `CFBundleShortVersionString` were being concatenated in the wrong order.

**iOS Acquisition release 2.0.2**

* Fixed a bug where a duplicate Analytics hit was sent when `ACPCore::CollectLaunchInfo` was called.

## August 15, 2019

The following updates were made in this release:

**Android Core 1.4.3**

* Fixed a bug where the database operation might fail on Android Q \(Android 10\).
* Fixed a crash that was happening on Android versions 8.0 and 8.1 and was related to Android's `TimeZoneNamesImpl`.

## August 8, 2019

The following updates were made in this release:

**iOS Target 2.1.3**

* Fixed a bug that, when prefetchContent is called with a nil callback, caused a crash in iOS.

## August 6, 2019

The following updates were made in this release:

**Android Core 1.4.2**

* Fixed a bug where the replacement value for token `{%~timestampz%}` might be created with the wrong locale.
* Added `getUniqueIdentifier()` to the `Event` object.

  This value is a globally unique identifier for every `Event`.

**iOS Target 2.1.2 and Android Target 1.1.2**

* `target.previewEnabled`, a new configuration Boolean key, has been added. This key is used to enable/disable Target Preview.

  If key is not provided, preview is enabled by default.

* Fixed an issue in Android where Target Preview links were decoded twice, which lead to an error preview page.

## July 17, 2019

The following updates were made in this release:

**Android Core 1.4.1**

* Fixed an issue that, when making Analytics requests during the switch of Android activities, might result in incorrect Customer Perspective \(CP\) values.

## July 16, 2019

Adobe Experience Platform SDK for WeChat Mini Programs Beta

The Adobe Experience Platform SDK now supports WeChat Mini Programs. This beta release helps Adobe Analytics customers who want to track the behavioral usage of Mini Programs. For more information, see [the documentation](https://aep-sdks.gitbook.io/docs/beta/adobe-experience-platform-mini-programs-sdk) or contact your Adobe customer success manager.

## July 10, 2019

The following updates were made in this release:

**Android Griffon Bridge 1.0.2**

* Fixed bug where wildcard listener wasn't working.

## July 9, 2019

The following updates were made in this release:

**iOS Analytics 2.1.2**

* ACPAnalytics now correctly identifies Acquisition link event types.
* Fixes a compile-time error when using the “-all\_load” linker flag.

## June 28, 2019

The following updates were made in this release:

**Android Griffon Bridge 1.0.1**

* Initial beta release.

## June 27, 2019

The following updates were made in this release:

**iOS Target 2.1.1 and Android Target 1.1.1**

* Use the `target.propertyToken` configuration setting to configure the `at_property_token` that is generated from the Target UI, instead of passing the token as an mbox parameter.
* Fixed an issue where JSON offers were not being returned as content but instead default content was served.

## June 19, 2019

The following updates were made in this release:

**iOS Core release 2.3.2**

* Fixed an issue that, when making Analytics requests immediately after app launch, might result in incorrect Customer Perspective \(cp\) values.
* Fixed an issue that might cause the main thread to be blocked for up to 60 seconds while the app is shutting down.
* Fixed several issues leading to a non-observed crash in the background while the app attempts to shut down.

## June 13, 2019

The following updates were made in this release:

**iOS Core 2.3.1**

* Fixed an issue that was causing network request failures, which were introduced in version 2.2.2.
* Fixed an issue that might have caused crashes when the app was being shut down.
* Fixed an issue that might have caused the callback to be passed to `ACPCore start:` to be called before the EventHub has finished initialization.

## June 12, 2019

The following updates were made in this release:

**iOS Analytics 2.1.1:**

* Fixed a bug where the locale was incorrect for Analytics hits.
* Fixed a bug where the Analytics shared state was not updated with the visitor identifier.

## June 3, 2019

The following updates were made in this release:

**Android Core 1.4.0:**

* Fixed the migration of Custom Analytics ID from v4.
* Added the `collectMessageInfo` API to collect push/local notification-related data.
* Forced the \_\*\*\_usage of TLS v1.1/v1.2 on the Android 4.x devices \(Android API version from 16-19\).

**Android Signal 1.0.2:**

* Fixed an issue where the SSL connection was not kept alive.

**Android Identity 1.1.0:**

* Added the `getUrlVariables` API to retrieve Visitor Identifiers as URL-encoded query strings for hybrid mobile applications.

## May 31, 2019

The following updates were made in this release:

**iOS Core 2.3.0:**

* Fixed several crash issues.
* Fixed the migration of Custom Analytics ID from v4.
* Added the `collectMessageInfo` API to collect push/local notification-related data.
* Added the support for title and custom sound in local notifications.

**iOS Identity 2.1.0**

* Added the `getUrlVariables` API to retrieve Visitor Identifiers as URL-encoded query strings for hybrid mobile applications.

**iOS Campaign 1.0.2**

* Added enhanced alert reporting with clickthrough URL support in the Campaign response event.
* Added support for a custom title in local notifications.

## May 20, 2019

The following updates were made in this release:

**iOS Core 2.2.2**

* Fixed the issue where SSL connection was not kept alive.
* Added support for ISO 8601 timestamp for Rules Engine token replacement, you can use the placeholder `~timestampz`
* Fixed the bug where `ACPCore.getSdkIdentities` didn't return the correct value for Analytics visitor identifier \(VID\).
* Added support for migrating Privacy status from v4 to v5, if it was manually set with v4 SDK.
* Fixed issue where retrieving Privacy status may get delayed when device is offline.

**iOS Identity 2.0.3**

* Fixed issue where device locale was not properly read when creating network requests from Identity extension.
* Fixed issue where the callback was not called on `ACPIdentity.getIdentifiers` if no custom identifiers where synced previously.
* Fixed issue where the Analytics visitor identifier \(VID\) was not included in the `ACPIdentity.appendToUrl` callback value.

**Android Core 1.3.1**

* Added support for ISO 8601 timestamp for Rules Engine token replacement, you can use the placeholder `~timestampz`
* Fixed the bug where `MobileCore.getSdkIdentities` didn't return the correct value for Analytics visitor identifier \(VID\).
* Added support for migrating Privacy status from v4 to v5, if it was manually set with v4 SDK.
* Fixed issue where retrieving Privacy status may get delayed when device is offline.
* Added support for loading cached configuraiton and cached rules on subsequent launch.

**Android Identity 1.0.5**

* Fixed issue where the Analytics visitor identifier \(VID\) was not included in the `Identity.appendVisitorInfoForURL` callback value.

**Android Campaign 1.0.1**

* Added enhanced alert reporting with clickthrough URL support in the Campaign response event.
* Added support for a custom title in local notifications.

## May 15, 2019

**iOS Target 2.1.0 and Android Target 1.1.0**

* Upgraded the Target Delivery APIs to latest v1 delivery endpoint.
* Introduced `retrieveLocationContent`, a new API that retrieves content for multiple Target mbox locations simultaneously without increasing the reporting count for prefetch cases.
* Introduced `locationsDisplayed`, a new API that helps Target record location to display events.

  This API should only be used for prefetch scenarios.

* Provided support for `TargetParameters` which is a helper class that combines parameters such as `mboxParameters`, `profileParameters`, `orderParameters`, and `productParameters`.
* New `prefetchContent` and `locationClicked` APIs which accept TargetParameters.

## May 9, 2019

**iOS Analytics 2.1.0**

* Fixed a crash related to database multi-threading.
* Enforced HTTPs network requests.

React Native wrappers for the following extensions were pushed to npmjs:

* [Core, Identity, Lifecycle, and Signal](https://www.npmjs.com/package/@adobe/react-native-acpcore)
* [Analytics](https://www.npmjs.com/package/@adobe/react-native-acpanalytics)
* [Audience](https://www.npmjs.com/package/@adobe/react-native-acpaudience)
* [Campaign](https://www.npmjs.com/package/@adobe/react-native-acpcampaign)

## May 6, 2019

**Android Core 1.3.0**

* The `MobileCore.start()` API should only get called once, and the SDK ignores the subsequent calls to this API.
* Added an internal API for React Native support.

## May 2, 2019

The following updates were made in this release:

**iOS Core 2.2.1**

* Fixed an issue when the app network crashes under extreme conditions.

## April 26, 2019

The following updates were made in this release:

**iOS Core 2.2.0**

* The `ACPCore.start` API can only get called once.
* Added the `ACPCore.registerURLHandler` API, which allows the app to set a custom handler for click-through URLs.
* Fixed the problem where the SDK failed to get locale information.
* Allow the Rules Engine to replace the token for non-string objects.

**Android Core 1.2.2**

* Fixed a bug that prevented URLs from being correctly opened on some Android versions.

**iOS Analytics 2.0.4**

* Fixed a cocoapod dependency issue.

**iOS Mobile Services 2.0.1**

* Fixed a cocoapod dependency issue.

## April 16, 2019

Project Griffon is now available for beta access!

Project Griffon is a new, innovative product from Adobe to help you easily inspect, validate, debug data collection and experiences for your mobile app. Developed for app product managers and developers, Project Griffon ensures that your app is correctly implemented, which allows you to focus on creating engaging experiences.

Project Griffon is in beta, and the use of this beta release requires you to accept the terms outlined in [https://griffon.adobe.com](https://griffon.adobe.com).

If you need access, go to [https://griffon.adobe.com](https://griffon.adobe.com) and [register your interest](https://forms.office.com/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4UJN9zAhIEhJr3PBfyMf9wdUMjNHTjVCVUJXUDM0VUIzOUFWMk9RNlBLRC4u).

To learn more about Project Griffon, here are the links to the [documentation](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/project-griffon):

* [Set up Project Griffon](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/project-griffon/set-up-project-griffon)
* [Using Project Griffon](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/project-griffon/using-project-griffon)

## April 5, 2019

The following updates were made in this release:

**iOS Core 2.1.1**

* Core: Internal support for database scheme migration.
* Identity: Identity MID might be regenerated when privacy settings change from opted out to opted in/opt unknown in the same session.

**iOS Analytics 2.0.3**

* Fixed a minor Analytics hit ordering issue.

**iOS Mobile Services 1.0.0**

* Mobile Services \(mobilemarketing.adobe.com\) messaging and acquisition links is now supported through the new Mobile Services extension for the Adobe Experience Platform SDK.

## April 3, 2019

**iOS Campaign Standard 1.0.1**

* Fixed an issue with duplicate symbols being present in the Campaign extension library.

## March 25, 2019

The following updates were made in this release:

**iOS Core 2.1.0**

**Configuration**

If there is no cached configuration available, the SDK can fetch the configuration after a network restore.

**Core**

* Added the `ACPCore` log API, which allows third-party extensions and application developers to log messages and use the Mobile SDK `LogLevel` to select the verbosity of the logs.
* You can also use the ACPCore `getLogLevel` API to retrieve the current `LogLevel` that was set in the SDK.
* `trackAction` and `trackState` only accept `NSDictionary`-type context data.

## March 21, 2019

The **Adobe Campaign Standard** extension version 1.0.0 is now available for Android!

* This extension allows you to deliver and track in-app messages \(broadcast and personalized\) and push notifications to mobile app users from Adobe Campaign Standard.

**Android Core 1.2.1**

* Added protection around null results when `toString` is called on Intent extras data.

## March 20, 2019

The following updates were made in this release:

**Android Core 1.2.0**

The following updates were made to the Mobile Core extension in Android version 1.2.0:

**Configuration**

* If there is no cached configuration available, you can fetch the configuration after a network restore.
* Added environment-aware support, which allows you to define dev and stage environments in a property.

  **Important**: This overrides the config properties that were based on the default environment.

**Core**

* Added the `MobileCore.getApplication` API, which allows third-party extension developers access the application context.
* Added the `MobileCore.log` API, which allows third-party extensions and application developers to log messages and use the Mobile SDK `LoggingMode` to select the verbosity of the logs.
* You can also use the `MobileCore.getLogLevel` API to retrieve the current `LoggingMode` that was set in the SDK.

**Android Identity 1.0.4**

* You can regenerate the MID when privacy settings change from opted out to opted in/opt unknown in the same session.

## March 14, 2019

**Android Core 1.1.2**

* Resolved an issue that might result in a crash when the underlying Analytics database was corrupted.

## March 7, 2019

**Android Core 1.1.1**

* Resolved an issue that could result in a crash when the underlying Analytics database was corrupted.

## March 1, 2019

The following updates were made in this release:

**Android Core 1.1.0**

* The `setSmallIcon` and `setLargeIcon` APIs were added.

**Android Analytics 1.1.1**

* Use the `analytics.launchHitDelay` configuration setting to indicate how long to wait before Analytics launch hits are sent.

## February 28, 2019

The following updates were made to the **Adobe Target extension**:

The Target Client Code is now automatically added based on your Experience Cloud organization.

* If no code is found, you can type it in.
* If multiple codes are found, you can select the code from the drop-down list.

## February 20, 2019

The Adobe **Campaign Standard** extension version 1.0.0 is now available!

This extension allows you to deliver and track in-app messages \(broadcast and personalized\) and push notifications to mobile app users from Adobe Campaign Standard.

## February 19, 2019

**iOS Core 2.0.3**

* Bug fixes
* Added environment-aware support, which allows you to define dev and stage environments in a property.

  **Important**: This overrides the config properties that were based on the default environment.

## February 7, 2109

**iOS Core 2.0.2**

* Resolved an issue that caused failures when retrieving a configuration on application launch.

## January 24, 2019

The January 24th update includes changes to the Adobe Experience Platform Mobile SDKs and solution extensions for iOS applications. We provided an explanation of this change, why the changes were made, and how to update your application to include these changes.

### What

With this release, we have changed the Mobile SDK Core and all Adobe solution extensions from dynamic frameworks to static libraries.

### Why

Frameworks are an excellent way to package and distribute iOS dependencies but, in some situations, using frameworks can cause issues when a dependent framework is updated. All of the Adobe Experience Platform SDK extensions have a dependency on the Core extension. This means that when a change is made to the Mobile Core framework, all dependent extensions need to be rebuilt from the source. To resolve this issue, we changed the SDK Core and all Adobe solution extensions to use static libraries.

### How

There is nothing wrong or broken with the previous versions of the SDK. Apps that have already started development with the version 1.x SDK and extensions can continue in the development lifecycle with no impact. Mobile applications that have not yet started to implement the Mobile SDKs are also fine, as they will start out using the static libraries. The changes listed below are required for customers who have started implementing the Adobe Experience Platform Mobile SDK and want to update to the latest version.

{% hint style="info" %}
The changes are only for iOS.
{% endhint %}

To update existing Experience Platform Mobile SDK 1.x implementations to 2.x:

1. Use the latest installation instructions for your selected environment \(development, staging, production\).
2. Update your Pod file with the latest changes.
3. Run a 'pod update' command to pull in the latest version of the Mobile Core extension and any other solution extension updates.
4. In your app code, change all of your import statements:  

**For Objective-C**

Where you previously had imports that look like the following:

```text
   #import <ACPCore_iOS/ACPCore_iOS.h>
   #import <ACPIdentity_iOS/ACPIdentity_iOS.h>
   #import <ACPLifecycle_iOS/ACPLifecycle_iOS.h>
   #import <ACPSignal_iOS/ACPSignal_iOS.h>
   #import <ACPUserProfile_iOS/ACPUserProfile_iOS.h>
```

The imports will now drop the _iOS_ suffix and can be imported directly as follows:

```text
   #import "ACPCore.h"
   #import "ACPIdentity.h"
   #import "ACPLifecycle.h"
   #import "ACPSignal.h"
   #import "ACPUserProfile.h"
```

This change will hold true for any other Adobe solution extensions that you may have previously imported.

**For Swift**

Where you previously had imports that looked like:

```swift
   import ACPCore_iOS
   import ACPAnalytics_iOS
   import ACPIdentity_iOS
   import ACPLifecycle_iOS
   import ACPSignal_iOS
   import ACPUserProfile_iOS
```

The imports will now drop the _iOS_ suffix. Additionally, the Identity, Lifecycle and Signals extensions can be added just by importing core , for example:

```swift
    import ACPCore
    import ACPAnalytics
    import ACPUserProfile
```

We feel that this update will serve our customers and partners better in the long run. If you have any questions or issues, go to our [user forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk#).

## December 5, 2018

**iOS Core 1.1.1**

* Fixed a bug where the `deviceToken` conversion was incorrect in some situations.

## December 4, 2018

The following updates were made to all extensions:

**iOS version 1.1.0**

* All ACP frameworks now properly run on 32-bit devices.

## November 30, 2018

**iOS Core 1.0.2**

* Minor bug fixes

## November 20, 2018

The **Adobe Campaign Classic** extension version 1.0.0 is now available for iOS!

This extension enables the delivery and tracking of push notifications to mobile app users from Adobe Campaign Classic.

{% hint style="info" %}
This extension is only for Adobe Campaign Classic and will not work with Adobe Campaign Standard.
{% endhint %}

#### Key Features

In this release, you can:

* Send push tokens with information about the user and the device to Adobe Campaign Classic so that users can enable push messaging to mobile app users who opt in to notifications.
* Send additional custom profile data to Adobe Campaign Classic, which allows personalized push notifications.
* Track the receipt of push messages \(impressions\) in Android apps and silent notifications in iOS apps.
* Track when users click on push notifications.

Here is some additional information:

This extension is an alternative to the stand-alone Campaign Classic SDK. It allows Experience Platform SDK users to enable push messaging from Campaign Classic without installing the Campaign Classic SDK separately.

## November 16, 2018

The following updates were made to the Mobile Core extension:

**iOS version 1.0.1**

* Fixed a bug for extensions where the response callback was not called for the `dispatchEventWithResponseCallback` API.
* Minor bug fixes.

**Android version 1.0.5**

* This version now includes the _proguard-rules.pro_ config file.
* Minor bug fixes.

## September 27, 2018

Adobe Experience Platform SDKs are live!

* Version 1.0.0 of the Experience Platform SDKs were released for the Mobile Core, Analytics, Audience Manager, and Adobe Target extensions.

