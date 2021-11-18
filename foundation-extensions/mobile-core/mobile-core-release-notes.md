# Release Notes

## June 30, 2021

### iOS Core 2.9.4

* Fixed a Rules Engine bug affecting strings that contain the `&` character.
* Fixed a bug where JSON objects containing empty strings were not handled correctly.

## March 16, 2021

### iOS Core 2.9.3

* Fixed a Rules Engine bug affecting strings that contain regex escaping characters \(one of `*?+{`\) in the following matcher types:
  * Contains
  * Not Contains
  * Starts With
  * Ends With

## March 9, 2021

### iOS Core 2.9.2

* Update version for bundled ACPIdentity 2.5.1 and ACPLifecycle 2.2.1 release.

### iOS Identity 2.5.1

* Fixed a bug where the visitor URL variables was using a TS in milliseconds instead of seconds.

### iOS Lifecycle 2.2.1

* No longer generate invalid values for `Days Since Last Use`, `Days Since First Use` and `Days Since Last Upgrade` metrics when the time setting on the device is off.

## February 11, 2021

### iOS Core 2.9.1

* Fixed a crash which happened in `AdobeMarketingMobile::StringUtils`

## December 18, 2020

### iOS Core 2.9.0, iOS Identity 2.5.0, iOS Lifecycle 2.2.0, iOS Signal 2.2.0

* The AEP SDKs are now distributed using XCFrameworks in order to support hardware with the new Apple M1 architecture while maintaining support for existing Intel architecture.
  * **IMPORTANT**: Upgrading to XCFrameworks distribution requires Xcode 12.0 or newer
  * **IMPORTANT**: If using Cocoapods, upgrading to the XCFrameworks distribution requires Cocoapods 1.10.0 or newer

## December 2, 2020

### iOS Core 2.8.2

* Update version for bundled ACPIdentity 2.4.1 release.

### iOS Identity 2.4.1

* Fix issue where push identifier had incorrect value in Identity shared state when `setPushIdentifer` was not called on each launch.

## November 18, 2020

### iOS Core 2.8.1

* Fixed a memory alignment issue that caused crashes in iOS 10.x.

## November 4, 2020

### iOS Core 2.8.0

* Update version for bundled ACPIdentity 2.4.0 release.

### iOS Identity 2.4.0

* Added a `device_consent` status parameter when `setAdvertisingIdentifier` is called after ad tracking is enabled/disabled.
* The default Identity Server URL of `dpm.demdex.com` is used if the SDK configuration parameter `experienceCloud.server` is either missing or an empty string.

## October 21, 2020

### iOS Core 2.7.6

* Fixed several crashes that were happening during app shutdown.

## September 22, 2020

### iOS Core 2.7.5

* Fixes an issue where the EventHub could be blocked by synchronous network calls returning recoverable errors.

## September 10, 2020

### iOS Core 2.7.4

* Fixed an intermitted issue where third party extensions may experience crashes after unregistration when using the `ACPExtensionAPI`.

### iOS Lifecycle 2.1.2

* Added previous application Id and OS version info to lifecycle event data.

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

## July 16, 2020

### iOS Core 2.7.1

* Updated the wrapper type strings used by SDK plugins.
* Added support for the token `~timestampp` which complies with the Adobe Experience Platform Edge Network.
* Another attampt to fix the crash on `std::__1::system_error: mutex lock failed: Invalid argument`.

Released with ACPCore version 2.7.2 on Cocoapods

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

## April 21, 2020

The following updates were made in this release:

### iOS Core 1.6.1

* Added an internal enum for Cordova support.

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

## January 27, 2020

The following updates were made in this release:

### iOS Core 2.4.0

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

