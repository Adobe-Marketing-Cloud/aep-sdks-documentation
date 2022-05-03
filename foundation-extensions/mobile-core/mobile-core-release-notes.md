# Release Notes

## April 21, 2022

### Android Core 1.11.0

* Internal fixes to support In-App Messaging with the AEPMessaging extension.

### Android Identity 1.3.1

* Improved extension stability by adding additional error checks when processing sync identifier requests.

## April 8, 2022

### iOS AEPCore 3.5.0

* Adds two APIs to `Date+Format` class. Method `getISO8601UTCDateWithMilliseconds` formats a Date to string as with fractional seconds and UTC time zone, while `getISO8601FullDate` formats a Date to string with date without time using the local time zone.
* Lifecycle foreground and background events for Edge Network now format timestamps with fractional seconds and UTC time zone.
* Updates the timestamp format for rule token `~timestampp` with fractional seconds and UTC time zone. This rule token is used to set the mobile property data element "Adobe Experience Platform Timestamp".
* Improves Signal logging by treating all 2xx network responses as success.
* Fixes bug where dispatched events failed due to use of single quotes in name.
* Fixes format of push token string by uppercasing characters.

## March 11, 2022

### Android Core 1.10.1

* Updates the timestamp format for rule token `~timestampp`  with fractional seconds and UTC time zone. This rule token is used to set the mobile property data element "Adobe Experience Platform Timestamp". 

### Android Lifecycle 1.1.1

* Lifecycle foreground and background events for Edge Network now format timestamps with fractional seconds and UTC time zone. 

## February 14, 2022

### iOS Core 2.9.5
* Updates version for bundled ACPIdentity 2.5.2 release.

### iOS Identity 2.5.2
* Fixes intermittent issue for GetUrlVariables and AppendToUrl APIs when custom Analytics identifiers are being used.

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

## January 20, 2022

### iOS AEPCore 3.4.0
* Added support for a new API `clearUpdatedConfiguration()`, see Configuration API reference for more details.
* Added support for optionally capturing event history on the device.
* Added support for triggering rules engine conditions based on event history.

### iOS AEPServices 3.4.0
* Expanded configuration options for Fullscreen Messages.
* Added support for delegating in-app message delivery.

## December 22, 2021

### iOS AEPCore 3.3.2
* Stability improvements for Configuration extension and full screen messages.
* Configuration now allows for empty appId to reset the previously set appId value.
* Logging improvements for extensions registration flow.
* The Event Hub shares wrapper type in its shared state.
* Adds new messaging event type and sources.
* Deprecates SystemInfoService getApplicationVersion API.

### iOS AEPIdentity 3.3.2

* Fixes a bug where Identity.getIdentifiers API failed to encode the identifiers.
* Fixes intermittent issue for GetUrlVariables and AppendToUrl APIs when custom Analytics identifiers are being used.

### Android Core 1.9.2

* Fixed a bug where event number was not incremented correctly for shared states.
* Stability improvements for Configuration extension.
* Configuration now allows for empty appId to reset the previously set appId value.
* The Event Hub shares wrapper type in its shared state.

## December 15, 2021

### Android Core 1.9.1

* Fixed an issue that was causing duplicate query parameters in a deep link to be removed.

### Android Signal 1.0.4

* Bug fix to improve Signal stability.

## November 9, 2021 

### iOS AEPCore 3.3.1 

* Fixed a bug where Date was not persisted correctly in iOS versions less than 13. 

### iOS AEPLifecycle 3.3.1

* Added session start time to Lifecycle shared state. 

### iOS AEPIdentity 3.3.1 

* Fixed a bug where the default Experience Cloud ID server URL was not used when the `experienceCloud.server` configuration parameter was an empty string.

## Sept 3, 2021

### iOS AEPCore 3.3.0

* Added support for dispatch event rules consequence.

### iOS AEPLifecycle 3.3.0

* Lifecycle extension now dispatches two new events `applicationLaunch` and `applicationClose` which contain Mobile Lifecycle metrics in XDM format.
* Fixed an issue where application upgrades were detected based on changes in `CFBundleShortVersionString` instead of `CFBundleVersion`.

### Android Core 1.9.0

* Added support for dispatch event rules consequence.
* Added getFriendlyName API for third party extensions. 
* Specifies mutability for PendingIntent in the UIService in preparation for Android 12 changes.

### Android Lifecycle 1.1.0

* Lifecycle extension now dispatches two new events `applicationLaunch` and `applicationClose` which contain Mobile Lifecycle metrics in XDM format.

### Mobile Core Launch extension v2.1.20

* New `Foreground` and `Background` event types to be used in rules for triggering actions based on Mobile Application Lifecycle XDM events. 

## Aug 27, 2021

### Android Core 1.8.3

* Updated proguard rules to fix an issue which caused some extensions to not be registered correctly when using minification.

## Aug 18, 2021

### iOS AEPCore 3.2.4

* Fixed data race in `Event` and `ExtensionContainer` classes.
* Fixed a memory leak in `EventHub.registerResponseListener`.

## Jul 29, 2021

### iOS AEPCore 3.2.3

* Fixed an issue in the `PersistentHitQueue` where new hits can cause additional scheduled tasks.
* Improved handling of database errors in the `PersistentHitQueue`.

## June 30, 2021

### iOS AEPCore 3.2.2

* Remove double URL encoding of AEPIdentity identifiers.
* Prevent possible crash at shutdown in EventHub.

### iOS Core 2.9.4

* Fixed a Rules Engine bug affecting strings that contain the `&` character.
* Fixed a bug where JSON objects containing empty strings were not handled correctly.

## June 21, 2021

### iOS AEPCore 3.2.1

* Update version for bundled ACPIdentity 3.2.1 release.

## iOS AEPIdentity 3.2.1

* Fixed a bug where `Identity.syncIdentifier` and `Identity.syncIdentifiers` APIs would ignore the authentication state settings.

## June 8, 2021

### Android Core 1.8.2

* Fixed a bug in the `PersistentHitQueue` where hits would be retried earlier than desired in certain scenarios
* Fixed a bug where rule tokens with "&" were not handled correctly
* Minor change to how the SDK computes the operating system name

### Android Lifecycle 1.0.8

* Minor update to ensure compatibility with the latest Core 1.8.2

## June 7, 2021

### iOS AEPCore 3.2.0

* Support for handling identities request `Event`'s in AEPIdentity
* Improve public visiblity of `RuleConsequence`
* Added `getDeviceModelNumber` to `SystemInfoService`
* Various additions to `ThreadSafeDictionary`
* Added the ability to make a network request with raw data that is not UTF encoded
* Fixed a bug where condition definitions that did not contain a value were not handled correctly
* Introduced an API to set button image data to the `FloatingButton`
* Added `optimize` `EventType`
* Introduced an API to hide the `FullscreenMessage`
* Fixed a bug where token \(~ timestampu\) was not expanded correctly
* Introduced `webViewDidFinishLoading` to `FullScreenMessageDelegate`

> Note: This release introduces breaking changes to the `NetworkService` and the `SystemInfoService`.

## May 25, 2021

### Android Core 1.8.1

* Added support for Event encode/decode.

## May 6, 2021

### iOS AEPCore 3.1.3

* Update to use AEPRulesEngine 1.0.1.

### iOS AEPRulesEngine 1.0.1

* Fixed a Swift compatibility issue.

## April 29, 2021

### iOS AEPCore 3.1.2

* Fixed a bug where the URL session was not reused for the same host.
* Fixed a Swift compatibility issue.

### iOS AEPIdentity 3.1.2

* Fixed a bug where Identity was blocked on the first launch if the configuration was invalid.

## April 8, 2021

### iOS AEPCore 3.1.1

* Fixed a bug where incomplete eventhub shared state was created before the event hub has been started.

## April 1, 2021

### iOS AEPCore 3.1.0

* New API - `MobileCore.collectLaunchInfo()` - see API reference for more information.
* New API - `MobileCore.resetIdentities()` - see API reference for more information.
* Added multiple new values to `EventType` and `EventSource`.
* Fixed a bug causing regular listeners to receive paired response events.
* Fixed a bug preventing proper data migration from v4 and v5 SDK.
* The callback method passed to `MobileCore.registerEventListener` now runs on a background thread.
* Improved logging for dictionaries.
* The EventHub's shared state dictionary now uses the full name of each registered extension as its key.

### iOS AEPIdentity 3.1.0

* Fixed an issue where privacy status was not correctly loaded from persistence.
* Advertising ID can now correctly be set after having an initial value of "zeroes" or empty.

### iOS AEPServices 3.1.0

* Added support for UI Services.
* The Locale string used in HTTP Headers is now properly formatted.
* Fixed a bug that would sometimes prevent downloaded files from being properly unzipped.

### March 31, 2021

#### Android Core 1.8.0

* New API - Public platform services for network, data queue, device info.
* New API - `MobileCore.resetIdentities()` - See API Reference for more information
* New API - `MobileCore.dispatchEventWithResponseCallback()` - See API Reference for more information.
* The EventHub's shared state dictionary now uses the full name of each registered extension as its key.

#### Lifecycle Core 1.0.7

* No longer generate invalid values for `Days Since Last Use`, `Days Since First Use` and `Days Since Last Upgrade` metrics when the time setting on the device is off.

### March 16, 2021

#### iOS Core 2.9.3

* Fixed a Rules Engine bug affecting strings that contain regex escaping characters \(one of `*?+{`\) in the following matcher types:
  * Contains
  * Not Contains
  * Starts With
  * Ends With

### March 9, 2021

#### iOS Core 2.9.2

* Update version for bundled ACPIdentity 2.5.1 and ACPLifecycle 2.2.1 release.

#### iOS Identity 2.5.1

* Fixed a bug where the visitor URL variables was using a TS in milliseconds instead of seconds.

#### iOS Lifecycle 2.2.1

* No longer generate invalid values for `Days Since Last Use`, `Days Since First Use` and `Days Since Last Upgrade` metrics when the time setting on the device is off.

### February 24, 2021

#### Android Core 1.7.0

* Fixed a crash which was caused by the exception thrown from the Android okhttp library.
* Added new public APIs to set XDM shared state.
* Added a new API `MobileCore.configureWithFileInAssets()` which allows the app to use a config file in the app's Assets folder.

### February 11, 2021

#### iOS Core 2.9.1

* Fixed a crash which happened in `AdobeMarketingMobile::StringUtils`

### February 2, 2021

#### Android Core 1.6.0

* Added a new API `MobileCore.registerEventListener` which can be used to register a permanent event listener.
* Fixed a bug which prevented cached configuration being loaded during app launch.
* Fixed a crash which was caused by the exception thrown from the Android `okhttp` library.

## January 19, 2021

### Adobe Experience Platform iOS Core SDKs

The brand new Adobe Experience Platform Core iOS swift SDKs are live! It is [open sourced on github](https://github.com/adobe/aepsdk-core-ios/), containing the following extensions:

* AEPCore 3.0.0
* AEPServices 3.0.0
* AEPIdentity 3.0.0
* AEPSignal 3.0.0
* AEPLifecycle 3.0.0
* AEPRulesEngine 1.0.0

### December 18, 2020

#### iOS Core 2.9.0, iOS Identity 2.5.0, iOS Lifecycle 2.2.0, iOS Signal 2.2.0

* The AEP SDKs are now distributed using XCFrameworks in order to support hardware with the new Apple M1 architecture while maintaining support for existing Intel architecture.
  * **IMPORTANT**: Upgrading to XCFrameworks distribution requires Xcode 12.0 or newer
  * **IMPORTANT**: If using Cocoapods, upgrading to the XCFrameworks distribution requires Cocoapods 1.10.0 or newer

### December 3, 2020

#### Android Identity 1.2.2

* Fix issue where push identifier had incorrect value in Identity shared state when `setPushIdentifer` was not called on each launch.

  Released with sdk-core version 1.5.8

### December 2, 2020

#### iOS Core 2.8.2

* Update version for bundled ACPIdentity 2.4.1 release.

#### iOS Identity 2.4.1

* Fix issue where push identifier had incorrect value in Identity shared state when `setPushIdentifer` was not called on each launch.

### November 18, 2020

#### iOS Core 2.8.1

* Fixed a memory alignment issue that caused crashes in iOS 10.x.

### November 4, 2020

#### iOS Core 2.8.0

* Update version for bundled ACPIdentity 2.4.0 release.

#### iOS Identity 2.4.0

* Added a `device_consent` status parameter when `setAdvertisingIdentifier` is called after ad tracking is enabled/disabled.
* The default Identity Server URL of `dpm.demdex.com` is used if the SDK configuration parameter `experienceCloud.server` is either missing or an empty string.

### October 21, 2020

#### iOS Core 2.7.6

* Fixed several crashes that were happening during app shutdown.

### September 22, 2020

#### iOS Core 2.7.5

* Fixes an issue where the EventHub could be blocked by synchronous network calls returning recoverable errors.

### September 10, 2020

#### iOS Core 2.7.4

* Fixed an intermitted issue where third party extensions may experience crashes after unregistration when using the `ACPExtensionAPI`.

#### iOS Lifecycle 2.1.2

* Added previous application Id and OS version info to lifecycle event data.

## September 9, 2020

### Android Core 1.5.7

* Fixed the issue where it may fail to save caches when `Etag` contains special characters.

### Android Identity 1.2.1

* Report extension details to Mobile Core for improved logging and Griffon support.
* Identity shared state now gets updated in current session on server response changes for blob or locationHint.
* In order to improve the Analytics push tracking reports, the push notification preferences \(`a.push.optin`\) are now forwarded to Analytics whenever the value passed to `setPushIdentifier` is different than the previous time it was called.
* Improved existing log messages and added additional logging to assist with debugging.

### Android Lifecycle 1.0.6

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

