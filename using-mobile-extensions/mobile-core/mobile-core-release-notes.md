# Release Notes

## September 9, 2020
### Android Identity 1.2.1
* Report extension details to Mobile Core for improved logging and Griffon support.
* Identity shared state now gets updated in current session on server response changes for blob or locationHint.
* In order to improve the Analytics push tracking reports, the push notification preferences \(`a.push.optin`\) are now forwarded to Analytics whenever the value passed to `setPushIdentifier` is different than the previous time it was called.
* Improved existing log messages and added additional logging to assist with debugging.

## Aug 10, 2020

### iOS Core 2.7.2 \(Released with ACPCore version 2.7.3 on Cocoapods\)

* Fixed a crash happening on `AdobeMarketingMobile::RulesEngine::ProcessEventForRules()`.
* Fixed an issue where null values in rules consequences were not respected.

### iOS Identity 2.3.2

* Identity shared state now gets updated in current session on server response changes for blob or locationHint.
* In order to improve the Analytics push tracking reports, the push notification preferences \(`a.push.optin`\) are now forwarded to Analytics whenever the value passed to `setPushIdentifier` is different than the previous time it was called.
* Improved safety checks for the Identity APIs with completion handler.

### iOS Lifecycle 2.1.1

* Session start time is now added to the shared state of Lifecycle extension.

## July 31, 2020

### Android Core 1.5.6

* Fixed an issue where null values in rules consequences was not respected.
* Some internal fixes.

### Android Lifecycle 1.0.5

* Session start time is now added to the shared state of Lifecycle extension.

## July 16, 2020

### iOS Core 2.7.1

* Updated the wrapper type strings used by SDK plugins.
* Added support for the token `~timestampp` which complies with the Adobe Experience Platform Edge Network.
* Another attampt to fix the crash on `std::__1::system_error: mutex lock failed: Invalid argument`.

Released with ACPCore version 2.7.2 on Cocoapods

### Android Core 1.5.5

* Updated the wrapper type strings used by SDK plugins.
* Added support for the token `~timestampp` which complies with the Adobe Experience Platform Edge Network.

## June 26, 2020

### iOS Identity 2.3.1

* Fixed an intermittent bug where Identity data was not loading at SDK initialization time.

Released with ACPCore version 2.7.1 on Cocoapods

## June 17, 2020

### iOS Core 2.7.0

* Added tvOS compatibility
* Version 2.7.0 onwards, binaries are built with Xcode 11.0
* Fixed a crash which happened in AdobeMarketingMobile::ModuleEventListenerBase

### iOS Lifecycle 2.1.0

* Added tvOS compatibility
* Version 2.1.0 onwards, binaries are built with Xcode 11.0

### iOS Signal 2.1.0

* Added tvOS compatibility
* Version 2.1.0 onwards, binaries are built with Xcode 11.0

### iOS Identity 2.3.0

* Added tvOS compatibility
* Version 2.3.0 onwards, binaries are built with Xcode 11.0

## May 28, 2020

The following updates were made in this release:

### iOS Core 2.6.2

* Added the capability for rules engine to reprocess the events that are dispatched before rules are loaded.
* Fixed the import statement in `ACPNetworkServiceOverrider.h`.

### Android Core 1.5.4

* Added the capability for rules engine to reprocess the events that are dispatched before rules are loaded.
* Fixed a bug where the shared state of event hub was not properly created.
* Fixed a security issue.

## April 21, 2020

The following updates were made in this release:

### iOS Core 1.6.1

* Added an internal enum for Cordova support.

### Android Core 1.5.3

* Fixed a performance issue where the initiliaztion of SDK extensions could block the main thread for a while.

## April 9, 2020

The following updates were made in this release:

### Android Core 1.5.2

* Fixed several security issues.
* Improved existing log messages and added additional logging to assist with debugging.

### Android Lifecycle 1.0.3

* Fixed a bug where the `Resolution` was captured in non-English numerals.

## April 2, 2020

The following updates were made in this release:

### iOS Core 2.6.0

* Added support for overriding internal network stack with customer-provided implementation. For more information, see [Override network stack](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/platform-services#ios).

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

## February 4, 2020

The following updates were made in this release:

### Android Core 1.5.0

* Fixed a cursor leak.
* Mobile Core now shares the list of enabled extensions and their meta data through shared state.
* Fixed an issue where the advertising identifier was duplicated in the response to the `MobileCore.getSDKIdentifiers` API.
* Added support for overriding internal network stack with customer-provided code.
* Added a new interface with failure callback, `AdobeCallbackWithError`, which can be used with the `MobileCore.getPrivacyStatus`, `MobileCore.getSdkIdentities` methods.

  We plan to gradually add the ability to enable failure callback to the other extensions.

### Android Identity 1.2.0

* Added support for the optional `AdobeCallbackWithError` callback that is available in Android Core version 1.5.0 on the following APIs:

  * `appendVisitorInfoForURL`
  * `getUrlVariables`
  * `getIdentifiers`
  * `getExperienceCloudId`

  When the `AdobeCallbackWithError` is used, and you are retrieving the Mobile SDK values, the timeout value is 500ms; if the operation times out or is not successful, an `AdobeError` is returned.

Released with sdk-core version 1.5.0.

## January 27, 2020

The following updates were made in this release:

**iOS Core 2.4.0**

* Added a new property, `eventUniqueIdentifier`, to the `ACPExtensionEvent` class. 
* Fixed an issue where the advertising identifier was duplicated in the response of the `getSDKIdentifiers` API.
* Fixed an issue where the SDK was trying to download the rules multipile times immediately after app launch.
* Fixed a crash on `std::__1::system_error: mutex lock failed: Invalid argument`.
* Fixed a bug where the iOS fullscreen message was unable to load cached images.

## November 15, 2019

The following updates were made in this release:

### iOS Identity 2.1.3

* Synced custom and advertising identifiers with nil or empty values are now cleared from Identity shared state and local storage. They are also not synced with the Experience Cloud ID \(ECID\) Service.
* Fixed a threading issue where the Experience Cloud ID \(ECID\) Service response was handled on an incorrect thread potentially causing a memory corruption crash.

These changes were released as part of ACPCore CocoaPod v2.3.6.

## October 25, 2019

The following updates were made in this release:

### iOS Core 2.3.5

* Added support for attach data rules consequence.
* Added support for a boolean-type comparison for the Exist or Not Exist rules condition.

### Android Core 1.4.5

* Added support for attach data rules consequence.
* Added support for a boolean-type comparison for the Exist or Not Exist rules condition.
* Fixed a bug where the Exist and Not Exist rules condition might not work for a List or Map type value.
* Fixed a bug that, when fetching the remote config from Launch, might cause a crash on some Android devices.
* Fixed a bug that, when the data URL of an activity did not contain valid schema, might cause a crash.

### Android Identity 1.1.2

* Fixed a bug where the default Experience Cloud Server hostname is now used when no value is configured in the SDK.
* Fixed a bug where multiple custom identifiers with same idType value were synced with the Visitor ID Service.
* Custom visitor identifiers can now be cleared from the SDK by providing a null/empty identifier value for a previously synced idType.

## October 4, 2019

The following updates were made in this release:

### iOS Core 2.3.4

* Fixed a crash that might have happened during app shutdown..    
* Fixed a bug where, when the SDK is being used in multiple threads, the SDK might not function under a race condition..    
* Fixed a bug where the downloaded rules zip file might not be decompressed.    
* Fixed a bug where the getSdkIdentities API used wrong key names for the Push ID and IDFA.    
* Removed the usage of UIWebView.    
* Extension listeners with null/empty type or source is now invalid and will not be registered.    

### iOS Identity 2.1.2

* Fixed an issue where the push identifier is not contained in the Identity shared state on bootup.    
* Fixed an issue where appendToUrl uses the incorrect query delimiter when the source URL contains a question mark in its fragment identifier component.

## September 17, 2019

The following updates were made in this release:

### Android Core 1.4.4

* Starting in API level 16, notifications now support BigTextStyle.
  * This enables long notifications to be displayed without being truncated.
* Fixed the locale string in the HTTP User-Agent to follow the BCP 47 specification.

## September 9, 2019

The following updates were made in this release:

### Android Identity 1.1.1

* Custom identifiers with null or empty IDs are ignored when calling the syncIdentifier or syncIdentifiers APIs because the Visitor ID Service does not support these identifiers.
* The syncIdentifiers API call is ignored when there is an empty Map.
* The duplicate advertising identifier value is removed from the Identity-shared state when MobileCore.setAdvertisingIdentifier is called with a new value.
* The global.ssl configuration settings are ignored, and SSL is enabled by default.
* Fixed an issue where appendVisitorInfoForURL uses the wrong query delimiter when the source URL contains a question mark in its fragment identifier component.

