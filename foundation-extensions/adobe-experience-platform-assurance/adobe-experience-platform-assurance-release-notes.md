# Release Notes

Release notes and change logs for the Adobe Experience Platform Assurance extension

## June 28, 2021

### iOS AEPAssurance 3.0.0

* Initial release to support [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) for Adobe Experience Platform Mobile SDKs for iOS in Swift. This library as available as an [open sourced project on Github](https://github.com/adobe/aepsdk-assurance-ios).

## June 17, 2021

### iOS Assurance 1.1.3

- Assurance state is now properly shared when reconnecting to an established session.

### Android Assurance 1.0.3

* Assurance state is now properly shared when reconnecting to an established session.
---

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
---

## December 18, 2020

### iOS Assurance 1.1.0

* The AEP SDKs are now distributed using XCFrameworks in order to support hardware with the new Apple M1 architecture while maintaining support for existing Intel architecture.
  * **IMPORTANT**: Upgrading to XCFrameworks distribution requires Xcode 12.0 or newer
  * **IMPORTANT**: If using Cocoapods, upgrading to the XCFrameworks distribution requires Cocoapods 1.10.0 or newer
---

## November 24, 2020

### Android Assurance 1.0.1

* Fixed a bug that triggered ANR \(Application not responsive\) error while initializing webview.
---

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
---

## October 05, 2020

### iOS Assurance 1.0.0

* General availability and release of [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) that enables capabilities of [Project Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon)

### Android Assurance 1.0.0

* General availability and release of [Adobe Experience Platform Assurance](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-experience-platform-assurance) that enables capabilities of [Project Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon)
