---
description: Release notes and change logs for the Adobe Experience Platform Mobile SDKs.
---

# Release notes

## April 13, 2021

### Identity Launch Extension

You can now find the `Identity` extension in the Launch extensions catalog for mobile properties.

## April 12, 2021

### Consent Launch Extension

You can now find the `Consent` extension in the Launch extensions catalog for mobile properties.

## April 8, 2021

### iOS AEPCore 3.1.1

* Fixed a bug where incomplete eventhub shared state was created before the event hub has been started.

### iOS AEPEdge 1.1.0

- Integration with AEPEdgeConsent 1.0.0 and collect consent preferences enforcement on requests to AEP Edge Network.
- Adds required dependency on AEPEdgeIdentity 1.0.0 that brings XDM IdentityMap support for custom identifiers.

### Android Edge 1.1.0

- Integration with edgeconsent 1.0.0 and collect consent preferences enforcement on requests to AEP Edge Network.
- Adds required dependency on edgeidentity 1.0.0 that brings XDM IdentityMap support for custom identifiers.

### iOS & Android Identity 1.0.0

The Adobe Experience Platform Identity (AEPEdgeIdentity\) mobile extension is now available on iOS and Android! This extension enables handling of user identity data from a mobile app when using the Adobe Experience Platform SDK and the Edge Network extension.

## April 5, 2021

### iOS & Android Consent 1.0.0

The Adobe Experience Platform Consent (AEPEdgeConsent\) mobile extension is now available in iOS and Android! This extension enables consent preferences collection from your mobile app when using the Adobe Experience Platform Mobile SDK and the Edge Network extension. You can now find the `Consent` extension in the Launch extensions catalog for mobile properties.

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

## January 19, 2021

### Adobe Experience Platform iOS Core SDKs

The brand new Adobe Experience Platform Core iOS swift SDKs are live! It is [open sourced on github](https://github.com/adobe/aepsdk-core-ios/), containing the following extensions:

* AEPCore 3.0.0
* AEPServices 3.0.0
* AEPIdentity 3.0.0
* AEPSignal 3.0.0
* AEPLifecycle 3.0.0
* AEPRulesEngine 1.0.0

### iOS AEPEdge 1.0.0

The Adobe Experience Platform Edge Network \(AEPEdge\) mobile extension is now available in iOS! This extension allows for sending XDM formatted data to Adobe Experience Platform and Adobe Experience Cloud solutions, by leveraging Experience Edge capabilities.

The included features with this release are:

* Ability to create XDM Experience Events and send them to Experience Edge Network. An optional Experience Edge response callback can be registered per event.
* The XDM Experience Events can be sent to individual Adobe Experience Platform datasets when a custom dataset identifier is set at event level.
* Events persistence.
* ECID is automatically attached on each XDM Experience Event request.
* Integration with AEPAssurance extension enabling new insights in Project Griffon about the XDM Experience Event processing and XDM data validation for an improved validation and debugging experience. 
* Detailed warning/error messages are available through Project Griffon UI and logs.

Learn more about the AEP Edge extension in the open sourced [adobe/aepsdk-edge-ios](https://github.com/adobe/aepsdk-edge-ios) GitHub repository. The iOS SDK is available for installation through SPM, XCFramework and Cocoapods and can be used in Swift and Objective-C applications. This SDK is compatible with latest swift AEPCore 1.0.0.

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

