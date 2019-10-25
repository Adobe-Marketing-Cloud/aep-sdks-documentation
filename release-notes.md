# Release notes

Here are the release notes for the Experience Platform Mobile SDKs and Adobe Places:

**Important:** Adobe Places is currently in Beta. On the Places GA date, the Places release notes content will be removed from this release notes and the location to the Places release notes will be provided.

## October 25, 2019

The following updates were made in this release:

**Android Identity 1.1.2**

- Fixed a bug where the default Experience Cloud Server hostname is now used when no value is configured in the SDK.
- Fixed a bug where multiple custom identifiers with same `idType` value were synced with the Visitor ID Service.
- Custom visitor identifiers can now be cleared from the SDK by providing a null/empty identifier value for a previously synced `idType`.

## October 10, 2019

The following updates were made in this release:

**iOS Campaign Classic 2.0.1**

* Fixed an issue where, on iOS 13, the push token was not being extracted correctly from NSData during device registration.    
* Fixed an issue where the charset information was not being sent in the Content-Type header during device registration call.

## October 9, 2019 \(Places\)

* **PlacesMonitor 2.1.0 \(iOS\)**
  * Added a new API, `setRequestAuthorizationLevel`, to set the type of location authorization request for which the user will be prompted.
* **PlacesMonitor 2.1.0 \(Android\)**
  * Added a new API, `setLocationPermission`, to set the type of location permission request for which the user will be prompted.
  * The Places Monitor now supports Android 10.

## October 7, 2019

The following updates were made in this release:

**Android Analytics 1.2.1**

* Fixed a bug where the Analytics database was being modified by multiple threads on startup.

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

**Android Core 1.4.4**

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

**Android Identity 1.1.1**

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

* Fixed a bug where the database operation might fail on Android Q.
* Fixed a crash that was happening on Android versions 8.0 and 8.1 and was related to Android's `TimeZoneNamesImpl`.

## Aug 8, 2019 \(Places\)

The following updates were made in this release:

### Places UI Updates

Here is a list of the updates to the Places UI:

#### New Features

* Added a new list view that shows POIs without the map.
* Added POI filtering options for the city, the state, the country, and the metadata.
* The first library in an organization is automatically created.
* Added POI sorting to the List View.

#### UI Updates

* Moved the list and details panel to right side of UI.
* Added a new search panel to the top of the UI.
* If only one library is present, this library is automatically selected when you create a POI.
* Moved library management into a popup window.
* Added a POI count next to the filters.

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

## Aug 6, 2019 \(Places\)

The following updates were made in this release:

### Places Monitor Launch Extension 2.0.0

* Updated the Android and iOS installation instructions for the Places Monitor 2.0.

## July 31, 2019 \(Places\)

The following updates were made in this release:

### Places Monitor 2.0.0

* Monitoring status is now persisted between launches.
* The handling of the callback, which resulted from a location permission request no longer requires you to extend PlacesActivity.
* Changed an existing API, allowing developers to clear all Places data from the device:

  Old API: `public static void stop();`

  New API: `public static void stop (final boolean clearData);`

* Updated the use of the Places `getNearbyPointsOfInterest` API to handle error scenarios more effectively.

## July 25, 2019 \(Places\)

The following updates were made in this release:

### ACPPlacesMonitor 2.0.0

* To clear all Places data from the device,

  in ACPPlacesMonitor, replaced an existing API `+ (void) stop;` with`+ (void) stop: (BOOL) clearData;`.

* Updated the use of the ACPPlaces `getNearbyPointsOfInterest` API to handle error scenarios more effectively.

## July 22, 2019 \(PLaces\)

The following updates were made in this release:

### Android Places 1.3.0

* Added a new API that clears out all Places-related data from shared state, in-app memory, and Shared Preference.
* Fixed an issue where shared state was not getting updated during application start.
* Fixed a bug where `getNearbyPointsOfInterest` callback was returning error code `SERVER_RESPONSE_ERROR instead of CONNECTIVITY_ERROR` on no internet.
* `getNearbyPointsOfInterest` API \(without the errorCallback\) will have the `successCallback` called with empty poi list, in case of error retrieving the nearby points of interest.

## July 19, 2019 \(Places\)

The following updates were made in this release:

**iOS Places 1.2.0**

Added a new API that clears out all Places-related data from shared state, in-app memory, and `NSUserDefaults`.

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

## June 25, 2019 \(Places\)

The following updates were made in this release:

**iOS Places Monitor 1.0.2**

* Quality of life improvements, including better in-code documentation and logging.

## June 19, 2019

The following updates were made in this release:

**iOS Core release 2.3.2**

* Fixed an issue that, when making Analytics requests immediately after app launch, might result in incorrect Customer Perspective \(cp\) values.
* Fixed an issue that might cause the main thread to be blocked for up to 60 seconds while the app is shutting down.
* Fixed several issues leading to a non-observed crash in the background while the app attempts to shut down.

## June 17, 2019 \(Places\)

The following updates were made in this release:

**iOS Places 1.1.0**

* Added a new API to return an error code when there is a failure retrieving nearby places.
* When privacy status changes to opt-out, all Places-related data will now be wiped from the device.
* Fixed an issue that, after a first launch, sometimes caused Places events to be lost due to bad network conditions.
* Fixed an issue where, when processing POI entry events in quick succession, token replacement via Rules Engine sometimes reference the incorrect POI.

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

## May 30, 2019 \(Places\)

**Android Places Monitor 1.0.1**

* Fixed an issue that prevented an entry event for POIs when the Places monitoring is started.

## May 28, 2019 \(Places\)

Fixed the following issues in the Places UI:

* Updated the Solution Switcher in Places to align with the rest of the Experience Cloud.
* Fixed an issue where rank was saving in instances where no rank changes were made.
* Increased the minimum allowed radius in the UI to 10 meters.
* Fixed an issue where, if you delete all the numbers in the field, the radius field reset back to 20 meters.

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

## May 17, 2019 \(Places\)

The following updates were made in this release:

**Android Places 1.2.0**

* Added a new API to process an individual `Geofence`.
* Bug fix to prevent multiple consecutive entry events.

**Android Places Monitor 1.0.0**

Initial release of the Places Monitor for Android.

The Places Monitor manages the OS-level Location APIs and communicates directly with the Places extension. With both extensions installed, customers can have out-of-the-box region monitoring in their application.

For more information about the Places Monitor, [click here](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/7ad91dd281c187baadf3698a3130f4ac0ef81fbe/places-extension-1/places-monitoring-extension/README.md).

## May 15, 2019

**iOS Target 2.1.0 and Android Target 1.1.0**

* Upgraded the Target Delivery APIs to latest v1 delivery endpoint.
* Introduced `retrieveLocationContent`, a new API that retrieves content for multiple Target mbox locations simultaneously without increasing the reporting count for prefetch cases.
* Introduced `locationsDisplayed`, a new API that helps Target record location to display events.

  This API should only be used for prefetch scenarios.

* Provided support for `TargetParameters` which is a helper class that combines parameters such as `mboxParameters`, `profileParameters`, `orderParameters`, and `productParameters`.
* New `prefetchContent` and `locationClicked` APIs which accept TargetParameters.

**Android Places 1.1.0**

* Introduced a new API for `getNearByPlaces`, which has an `errorCallback` and is called with an `errorCode` that indicates the reason for the error.    
* Introduced a new API for `getNearByPlaces`, which has an `errorCallback` and is called with an `errorCode` that indicates the reason for the error.
* The Places extension now queues the events until a configuration is obtained.    
* The Places extension now queues the events until a configuration is obtained.

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

**Android Places 1.1.0**

* Introduced a new API for `getNearByPlaces`, which has an `errorCallback` and is called with an `errorCode` that indicates the reason for the error.
* The Places extension now queues the events until a configuration is obtained.
* Added support for environment-aware configurations.
* Bug Fix : corrected the keys for the region entry/exit events
* Storage of last known location now properly respects the user's privacy status

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

## April 9, 2019 \(Places\)

The following updates were made in this release:

**iOS Places Monitor 1.0.1**

* Added full unit test coverage.
* CI integration \(CircleCI\).
* Code coverage integration \(codecov\).

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

**iOS Places Monitor 1.0.0**

Initial release of the **Places Monitor** for iOS.

The Places Monitor manages the OS-level Location APIs and communicates directly with the Places extension. With both extensions installed, customers can have out-of-the-box region monitoring in their application.

For more information about the Places Monitor, [click here](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/7ad91dd281c187baadf3698a3130f4ac0ef81fbe/places-extension-1/places-monitoring-extension/README.md).

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

## February 28, 2019 \(Places\)

The first version of **Places** is now available for public beta access!

The Places solution is composed of the following components:

* The **Places Services** is a robust set of REST APIs that provide an interface to the database that stores all Places-related data for a customer. For more information, see [Places database management](https://launch.gitbook.io/places-services-by-adobe-documentation/places-database-management-1).
* A **Places-specific card** on Adobe IO \(coming soon\).
* The **Places UI** is built on the APIs that are provided by the Places Service and allows customers to create and manage their Places libraries.

  To log in to the Places UI, go to [https://places.adobe.com](https://places.adobe.com).

* The **Places Extension \(Experience Platform Launch and SDK\)** The functionality in the extension retrieves the relevant Places data from the Places Services based on the location of the calling device. The SDK extension also dispatches Places-related events on the Event Hub for consumption by the Rules Engine and other interested extensions:
  * **GitHub**: [https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/tag/v1.0.0-ACPPlaces](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/tag/v1.0.0-ACPPlaces)
  * **Cocoapod**: [https://cocoapods.org/pods/ACPPlaces](https://cocoapods.org/pods/ACPPlaces)
  * **Maven Central**: [https://mvnrepository.com/artifact/com.adobe.marketing.mobile/places](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/places)

### Documentation Links

To learn more about Places, here are links to the documentation:

* UI - [https://launch.gitbook.io/places-services-by-adobe-documentation/](https://launch.gitbook.io/places-services-by-adobe-documentation/)
* SDK - [https://aep-sdks.gitbook.io/docs/using-mobile-extensions/places-extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/places-extension)

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

