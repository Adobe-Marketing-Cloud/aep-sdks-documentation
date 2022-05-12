# Release Notes

Release notes and change logs for the Adobe Experience Platform Assurance extension

## April 2, 2022

### iOS AEPAssurance 1.1.4

* Fixed a bug that caused Assurance to not connect to a session if your iOS app's `info.plist` contains a property of type `date`.

Note: This release pertains to Assurance mobile extension that works with ACPCore

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

## January 14, 2022

### Flutter Assurance 2.0.1

- Updated the package to reference the Android library from Maven Central Repository.
- Migrated to the new Android APIs based on [FlutterPlugin](https://api.flutter.dev/javadoc/io/flutter/embedding/engine/plugins/FlutterPlugin.html).

## September 14, 2021

### Xamarin Assurance iOS 1.0.0

- iOS Assurance framework updated to 1.1.3

### Xamarin Assurance Android 1.0.0

- Android Assurance framework updated to 1.0.3

## August 23, 2021

### React Native Assurance 2.0.0

This major release introduces support for following:

- Support for React Native version 0.60.+
- Auto linking for native dependencies and removal of the bundled SDK binaries (XCFramework) from the React Native module.
- Dynamic versions for native dependencies to always load the latest SDK.
- Removal of registerExtension Javascript API.

## August 18, 2021

### Flutter Assurance 2.0.0

- Updated to support Flutter 2.0 and null safety.

## June 28, 2021

### iOS AEPAssurance 3.0.0

* Initial release to support [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) for Adobe Experience Platform Mobile SDKs for iOS in Swift. This library as available as an [open sourced project on Github](https://github.com/adobe/aepsdk-assurance-ios).

## June 17, 2021

### iOS Assurance 1.1.3

* Assurance state is now properly shared when reconnecting to an established session.

### Android Assurance 1.0.3

* Assurance state is now properly shared when reconnecting to an established session.

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

## December 18, 2020

### iOS Assurance 1.1.0

* The AEP SDKs are now distributed using XCFrameworks in order to support hardware with the new Apple M1 architecture while maintaining support for existing Intel architecture.
  * **IMPORTANT**: Upgrading to XCFrameworks distribution requires Xcode 12.0 or newer
  * **IMPORTANT**: If using Cocoapods, upgrading to the XCFrameworks distribution requires Cocoapods 1.10.0 or newer

## November 24, 2020

### Android Assurance 1.0.1

* Fixed a bug that triggered ANR \(Application not responsive\) error while initializing webview.

## November 23, 2020

### React Native Assurance 1.0.0

* AEP Assurance extension released for React Native. See: [Assurance React Native](https://www.npmjs.com/package/@adobe/react-native-aepassurance)

### Flutter Assurance 1.0.1

* AEP Assurance extension released for Flutter. See: [Assurance Flutter](https://pub.dev/packages/flutter_assurance)

### Xamarin Assurance 0.0.1

* AEP Assurance extension released for Xamarin iOS. See : [Assurance Xamarin iOS](https://www.nuget.org/packages/Adobe.AEPAssurance.iOS/)
* AEP Assurance extension released for Xamarin Android. See : [Assurance Xamarin Android](https://www.nuget.org/packages/Adobe.AEPAssurance.Android/)

### Cordova Assurance 0.0.1

* AEP Assurance extension released for Cordova. See : [Assurance Cordova](https://www.npmjs.com/package/@adobe/cordova-aepassurance)

### Unity Assurance 0.0.1

* AEP Assurance extension released for Unity. See: [Assurance Unity](https://github.com/adobe/unity-aepassurance)

## October 05, 2020

### iOS Assurance 1.0.0

* General availability and release of [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) that enables capabilities of [Project Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon)

### Android Assurance 1.0.0

* General availability and release of [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) that enables capabilities of [Project Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon)
