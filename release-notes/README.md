---
description: Release notes and change logs for the Adobe Experience Platform Mobile SDKs.
---

# Release notes

## Jul 13, 2021

### iOS AEPAudience 3.0.2

* Added support to handle MobileCore.resetIdentities() API.

## Jul 2, 2021

### iOS AEPUserProfile 3.0.1

* Fixed a bug preventing proper data migration when presented with an `app group` .

## June 30, 2021

### iOS AEPCore 3.2.2

* Remove double URL encoding of AEPIdentity identifiers.
* Prevent possible crash at shutdown in EventHub.

## June 28, 2021

### iOS AEPAssurance 3.0.0

* Initial release to support [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) for Adobe Experience Platform Mobile SDKs for iOS in Swift. This library as available as an [open sourced project on Github](https://github.com/adobe/aepsdk-assurance-ios).

## June 24, 2021

### iOS ACPPlacesMonitor 2.1.4

* Update to iOS 14 method for retrieving `CLAuthorizationStatus`.
* Updating README.md with notice of deprecation on August 31, 2021.

## June 22, 2021

### iOS Core 2.9.4

* Fixed a Rules Engine bug affecting strings that contain the `&` character.
* Fixed a bug where JSON objects containing empty strings were not handled correctly.

## June 21, 2021

### iOS AEPCore 3.2.1

* Update version for bundled ACPIdentity 3.2.1 release.

## iOS AEPIdentity 3.2.1

* Fixed a bug where `Identity.syncIdentifier` and `Identity.syncIdentifiers` APIs would ignore the authentication state settings.

## June 17, 2021

### iOS Assurance 1.1.3

- Assurance state is now properly shared when reconnecting to an established session.

### Android Assurance 1.0.3

* Assurance state is now properly shared when reconnecting to an established session.

### iOS Messaging 1.0.0

* The Adobe Experience Platform Messaging \(AEPMessaging\) mobile extension is now available in iOS! This extension enables push notifications and measurement for Adobe Journey Optimizer. 

### Adobe Journey Optimizer Launch Extension

* You can now find the `Adobe Journey Optimizer` extension in the Launch extensions catalog for mobile properties.

## June 16, 2021

### Android Campaign 1.0.8

* Added the changes to move away from bintray and start using Sonatype to push the SDK to Maven Central.
* Resolved an issue with Campaign module details not being returned.

### Android Messaging 1.0.0

* The Adobe Experience Platform Messaging \(AEPMessaging\) mobile extension is now available in Android! This extension enables push notifications and measurement for Adobe Journey Optimizer.

## June 15, 2021

### Android Target 1.1.7

* Added the changes to move away from bintray and start using Sonatype to push the SDK to Maven Central.

## June 10, 2021

### iOS AEPEdge 1.1.1

* Development testing enhancements for Experience Edge.

### Android Edge 1.1.1

* Adds support for events persistence for use-cases with low network connectivity or unexpected network errors.
* Development testing enhancements for Experience Edge.

This SDK is compatible with Android Core 1.8.2 and above.

## June 8, 2021

### Android Core 1.8.2

* Fixed a bug in the `PersistentHitQueue` where hits would be retried earlier than desired in certain scenarios.
* Fixed a bug where rule tokens with "&" were not handled correctly.
* Minor change to how the SDK computes the operating system name.

### Android Lifecycle 1.0.8

* Minor update to ensure compatibility with the latest Core 1.8.2.

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

## Jun 4, 2021

### iOS AEPMobileServices 3.0.0

* Released the brand new Adobe Experience Platform Mobile Services iOS Swift SDK.

## May 25, 2021

### Android Core 1.8.1

* Added support for Event encode/decode.

## May 13, 2021

### Android Mobileservices 1.1.4

* Fixed a bug that caused a crash when multiple threads were accessing InAppMessages instance.

## May 10, 2021

### Android PlacesMonitor 2.2.2

* Fixed a crash that was caused when application did not find the required activity for requesting location permission.

## May 6, 2021

### iOS AEPCore 3.1.3

* Update to use AEPRulesEngine 1.0.1.

### iOS AEPRulesEngine 1.0.1

* Fixed a Swift compatibility issue.

## May 5, 2021

### iOS AEPMedia 3.0.0

* Initial release to support [Adobe Analytics - Media Analytics workflows](../using-mobile-extensions/adobe-media-analytics/) for Adobe Experience Platform Mobile SDKs for iOS in Swift. This extension library is [available as an open source project on Github](https://github.com/adobe/aepsdk-media-ios/).

## April 29, 2021

### iOS AEPCore 3.1.2

* Fixed a bug where the URL session was not reused for the same host.
* Fixed a Swift compatibility issue.

### iOS AEPIdentity 3.1.2

* Fixed a bug where Identity was blocked on the first launch if the configuration was invalid.

## April 21, 2021

### iOS Assurance 1.1.1

* Support for Shared States in XDM format when using the AEPEdge extension.
* Lifecycle install and launch hits are now captured for Adobe Analytics debugging.
* Sends extension-specific state events when connecting to a Griffon session.
* Better error handling when reaching activity or Griffon session limits.
* Bug fix that ensures the Griffon UI will always correctly show the number of connected devices.
* Various security fixes.

### Android Assurance 1.0.2

* Support for Shared States in XDM format when using the AEPEdge extension.
* Lifecycle install and launch hits are now captured for Adobe Analytics debugging.
* Sends extension-specific state events when connecting to a Griffon session.
* Better error handling when reaching activity or Griffon session limits.
* Various security fixes.

## April 14, 2021

### iOS Mobile Services 1.1.1

* Fixed a crash that could happen while downloading remote assets.

## April 13, 2021

### Identity for Edge Network

You can now find the Identity for Edge Network extension in the Launch extensions catalog for mobile properties.

## April 12, 2021

### Consent for Edge Network

You can now find the Consent for Edge Network extension in the Launch extensions catalog for mobile properties.

## April 8, 2021

### iOS AEPCore 3.1.1

* Fixed a bug where incomplete event hub shared state was created before the event hub has been started.

### iOS AEPEdge 1.1.0

* Integration with AEPEdgeConsent 1.0.0 and collect consent preferences enforcement on requests to AEP Edge Network.
* Adds required dependency on AEPEdgeIdentity 1.0.0 that brings XDM IdentityMap support for custom identifiers.

### Android Edge 1.1.0

* Integration with EdgeConsent 1.0.0 and collect consent preferences enforcement on requests to AEP Edge Network.
* Adds required dependency on EdgeIdentity 1.0.0 that brings XDM IdentityMap support for custom identifiers.

### iOS & Android Identity 1.0.0

The Adobe Experience Platform Identity \(AEPEdgeIdentity\) mobile extension is now available on iOS and Android! This extension enables handling of user identity data from a mobile app when using the Adobe Experience Platform SDK and the Edge Network extension.

## April 5, 2021

### iOS & Android Consent 1.0.0

The Adobe Experience Platform Consent \(AEPEdgeConsent\) mobile extension is now available in iOS and Android! This extension enables consent preferences collection from your mobile app when using the Adobe Experience Platform Mobile SDK and the Edge Network extension. You can now find the `Consent` extension in the Launch extensions catalog for mobile properties.

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

### iOS AEPAnalytics 3.0.1

* Added support to handle internal analytics track request events
* Refactored code and updated doc comments

### iOS AEPAudience 3.0.1

* Updated syncedVisitorIds implementation to a map
* Fixed access modifer for two classes

## March 31, 2021

### Android Core 1.8.0

* New API - Public platform services for network, data queue, device info.
* New API - `MobileCore.resetIdentities()` - See API Reference for more information
* New API - `MobileCore.dispatchEventWithResponseCallback()` - See API Reference for more information.
* The EventHub's shared state dictionary now uses the full name of each registered extension as its key.

### Android Lifecycle 1.0.7

* No longer generate invalid values for `Days Since Last Use`, `Days Since First Use` and `Days Since Last Upgrade` metrics when the time setting on the device is off.

## March 29, 2021

### Android Media 2.1.1

* Updated "Content-Type" header to “application/json” in Media Collection API requests.

## March 26, 2021

### iOS Media 2.3.1

* Updated "Content-Type" header to “application/json” in Media Collection API requests.

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

## February 26, 2021

### iOS AEPAnalytics 3.0.0

* Initial release to support [Adobe Analytics](../using-mobile-extensions/adobe-analytics/) for Adobe Experience Platform Mobile SDKs for iOS in Swift. This library as available as an [open sourced project on Github](https://github.com/adobe/aepsdk-analytics-ios/).

## February 24, 2021

### Android Core 1.7.0

* Fixed a crash which was caused by the exception thrown from the Android `okhttp` library.
* Added new public APIs to set XDM shared state.
* Added a new API `MobileCore.configureWithFileInAssets()` which allows the app to use a config file in the app's Assets folder.

## February 11, 2021

### iOS Core 2.9.1

* Fixed a crash which happened in `AdobeMarketingMobile::StringUtils`

## February 2, 2021

### Android Core 1.6.0

* Added a new API `MobileCore.registerEventListener` which can be used to register a permanent event listener.
* Fixed a bug which prevented cached configuration being loaded during app launch.
* Fixed a crash which was caused by the exception thrown from the Android `okhttp` library.

## January 29, 2021

### iOS Audience 3.0.0

* Initial release to support Adobe Audience for Adobe Experience Platform Mobile SDKs for iOS in Swift. This extension library is available as an [open sourced project on Github](https://github.com/adobe/aepsdk-audience-ios/).

## January 19, 2021

### Adobe Experience Platform iOS Core SDKs

Adobe Experience Platform Mobile SDKs for iOS are now being made available on Swift. Mobile Core in Swift is available as an [open sourced project on Github](https://github.com/adobe/aepsdk-core-ios/) and contains the following extensions:

* AEPCore 3.0.0
* AEPServices 3.0.0
* AEPIdentity 3.0.0
* AEPSignal 3.0.0
* AEPLifecycle 3.0.0
* AEPRulesEngine 1.0.0

### iOS AEPEdge 1.0.0

Initial release of Adobe Experience Platform Edge Network mobile extension iOS in Swift.

This extension allows for sending XDM formatted data to Adobe Experience Platform and Adobe Experience Cloud solutions, by leveraging Edge Network capabilities.

The included features with this release are:

* Ability to create XDM Experience Events and send them to Experience Edge Network. An optional Experience Edge response callback can be registered per event.
* The XDM Experience Events can be sent to individual Adobe Experience Platform datasets when a custom dataset identifier is set at event level.
* Events persistence.
* ECID is automatically attached on each XDM Experience Event request.
* Integration with AEPAssurance extension enabling new insights in Project Griffon about the XDM Experience Event processing and XDM data validation for an improved validation and debugging experience.
* Detailed warning/error messages are available through Project Griffon UI and logs.

This extension library is available as an open sourced project \([adobe/aepsdk-edge-ios](https://github.com/adobe/aepsdk-edge-ios)\) on GitHub.

These iOS libraries, written in Swift, are available for integration via SPM, XCFramework and Cocoapods and can be used in Swift and Objective-C applications.

### Android Edge 1.0.0

The Adobe Experience Platform Edge Network \(Edge\) mobile extension is now available in Android! This extension allows for sending XDM formatted data to Adobe Experience Platform and Adobe Experience Cloud solutions, by leveraging Experience Edge capabilities.

The included features with this release are:

* Ability to create XDM Experience Events and send them to Experience Edge Network. An optional Experience Edge response callback can be registered per event.
* The XDM Experience Events can be sent to individual Adobe Experience Platform datasets when a custom dataset identifier is set at event level.
* ECID is automatically attached on each XDM Experience Event request.
* Integration with Assurance extension enabling new insights in Project Griffon about the XDM Experience Event processing and XDM data validation for an improved validation and debugging experience.
* Detailed warning/error messages are available through Project Griffon UI and logs.

This SDK is compatible with Android Core 1.5.7 and above.

### Adobe Experience Platform Edge Network Launch Extension 1.0.2

* Selector for the Edge Configuration.
* AEP Request Event with optional XDM event type is available for Launch rules.

## January 20, 2021

### iOS Audience 2.3.0

* Added TVOS support to Audience.
