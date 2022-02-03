---
description: Release notes and change logs for the Adobe Experience Platform Mobile SDKs.
---

# Release notes

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

