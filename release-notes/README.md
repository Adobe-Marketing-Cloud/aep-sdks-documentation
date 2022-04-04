---
description: Release notes and change logs for the Adobe Experience Platform Mobile SDKs.
---

# Release notes

## April 1, 2022

### iOS AEPEdgeIdentity 1.0.1

* Synchronized updates and reads on the Identity for Edge Network shared state to avoid any race conditions.

### Adobe Experience Platform Edge Network Launch extension v1.1.9

- UI updates for the Datastream configuration section to enable the new datastreams support. If more than one sandbox is used, a sandbox picker is displayed to allow for datastreams selection across sandboxes.
- Auto-complete in the UI for default third party domain based on company name for Edge Network data collection. The domain configuration is now required, while existing configurations will continue to use the default edge.adobedc.net domain.

### Adobe Journey Optimizer Launch extension v0.0.16

- UI updates to support the new datastream selections in the AEP Edge Network extension.

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
