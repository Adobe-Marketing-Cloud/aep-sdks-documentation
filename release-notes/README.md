---
description: Release notes and change logs for the Adobe Experience Platform Mobile SDKs.
---

# Release notes

## Sep 20, 2021

### iOS 15 Compatibility

* All Adobe Experience Platform Mobile SDKs for iOS have been functionally validated to be compatible with iOS 15.

## Sep 17, 2021

### iOS Media 2.3.2

* Bug fixes to improve SDK stability.

## Sep 14, 2021

### Xamarin Assurance 1.0.0

* iOS Assurance framework updated to 1.1.3

* Android Assurance framework updated to 1.0.3

## Aug 23, 2021

### React Native Assurance 2.0.0

This major release introduces support for following:

* Support for React Native version 0.60.+
* Auto linking for native dependencies and removal of the bundled SDK binaries \(XCFramework\) from the React Native module.
* Dynamic versions for native dependencies to always load the latest SDK.
* Removal of registerExtension Javascript API.

## Aug 18, 2021

### Flutter Assurance 2.0.0

* Upgrade plugin to support Flutter 2.0 and null safety support.

## Aug 17, 2021

### Flutter Analytics 2.0.1

* Update to reference the Analytics Android library from mavenCentral.

## Aug 6, 2021

### Adobe Experience Platform Mobile SDK plugins for React Native

This major release introduces support for the following:

* React Native version 0.60.+
* Autolinking for native dependencies and removal of the bundled SDK binaries \(XCFramework\) from the React Native module.
* Dynamic versions for native dependencies to always load the latest SDK.
* Removal of several deprecated APIs.

Please note that this release introduces breaking changes. For more details, see the release notes of the following plugins:

* [@adobe/react-native-acpcore 2.0.0](https://github.com/adobe/react-native-acpcore/releases/tag/v2.0.0)
* [@adobe/react-native-acpuserprofile 2.0.0](https://github.com/adobe/react-native-acpuserprofile/releases/tag/v2.0.0)
* [@adobe/react-native-acpaudience 2.0.0](https://github.com/adobe/react-native-acpaudience/releases/tag/v2.0.0)
* [@adobe/react-native-acpanalytics 2.0.0](https://github.com/adobe/react-native-acpanalytics/releases/tag/v2.0.0)
* [@adobe/react-native-acpmedia 3.0.0](https://github.com/adobe/react-native-acpmedia/releases/tag/v3.0.0)
* [@adobe/react-native-acptarget 2.0.0](https://github.com/adobe/react-native-acptarget/releases/tag/v2.0.0)
* [@adobe/react-native-acpcampaign 2.0.0](https://github.com/adobe/react-native-acpcampaign/releases/tag/v2.0.0)
* [@adobe/react-native-acpplaces 2.0.0](https://github.com/adobe/react-native-acpplaces/releases/tag/v2.0.0)

## July 21, 2021

### iOS Analytics 2.5.1

* Removed retrieval and generation of Analytics tracking identifier \(AID\). Existing AID values stored on the device will continue to be loaded and used, however new visitors will not be assigned an AID value.

## June 24, 2021

### iOS ACPPlacesMonitor 2.1.4

* Update to iOS 14 method for retrieving `CLAuthorizationStatus`.
* Updating README.md with notice of deprecation on August 31, 2021.

## June 22, 2021

### iOS Core 2.9.4

* Fixed a Rules Engine bug affecting strings that contain the `&` character.
* Fixed a bug where JSON objects containing empty strings were not handled correctly.

## June 17, 2021

### iOS Assurance 1.1.3

* Assurance state is now properly shared when reconnecting to an established session.

## June 9, 2021

### Flutter

* Upgrade plugin to support Flutter 2.0 and null safety support for following packages:
* [flutter\_acpcore](https://pub.dev/packages/flutter_acpcore/versions/2.0.0)
* [flutter\_acpuserprofile](https://pub.dev/packages/flutter_acpuserprofile/versions/2.0.0)
* [flutter\_acpanalytics](https://pub.dev/packages/flutter_acpanalytics/versions/2.0.0)
* [flutter\_acpplaces](https://pub.dev/packages/flutter_acpplaces/versions/2.0.0)
* [flutter\_acpplaces\_monitor](https://pub.dev/packages/flutter_acpplaces_monitor/versions/2.0.0)

## April 21, 2021

### iOS Assurance 1.1.1

* Support for Shared States in XDM format when using the AEPEdge extension.
* Lifecycle install and launch hits are now captured for Adobe Analytics debugging.
* Sends extension-specific state events when connecting to a Griffon session.
* Better error handling when reaching activity or Griffon session limits.
* Bug fix that ensures the Griffon UI will always correctly show the number of connected devices.
* Various security fixes.

## April 14, 2021

### iOS Mobile Services 1.1.1

* Fixed a crash that could happen while downloading remote assets.

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

## February 11, 2021

### iOS Core 2.9.1

* Fixed a crash which happened in `AdobeMarketingMobile::StringUtils`

## January 20, 2021

### iOS Audience 2.3.0

* Added TVOS support to Audience.
