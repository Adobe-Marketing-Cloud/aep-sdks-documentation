# Release Notes

## June 16, 2021

### Android Campaign 1.0.8

* Added the changes to move away from bintray and start using Sonatype to push the SDK to Maven Central.
* Resolved and issue with Campaign module details not being returned.

## June 8, 2021

### iOS Campaign Standard 3.0.0

* Initial release to support [Adobe Campaign Standard workflows](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/master/using-mobile-extensions/adobe-campaign-standard) for Adobe Experience Platform Mobile SDKs for iOS in Swift. This extension library is [available as an open source project on Github](https://github.com/adobe/aepsdk-campaign-ios).

## December 18, 2020

### iOS Campaign Standard 1.1.0

* The AEP SDKs are now distributed using XCFrameworks in order to support hardware with the new Apple M1 architecture while maintaining support for existing Intel architecture.
  * **IMPORTANT**: Upgrading to XCFrameworks distribution requires Xcode 12.0 or newer
  * **IMPORTANT**: If using Cocoapods, upgrading to the XCFrameworks distribution requires Cocoapods 1.10.0 or newer

## September 29, 2020

The following updates were made in this release:

**Android Campaign 1.0.7 and iOS Campaign 1.0.6**

* Added an enhancement to reduce the number of registration requests sent to Campaign. There is now a default 7 day registration delay which starts after the most recent registration request sent to Campaign is successful.
* Added configuration settings to change the default registration delay or to pause registration requests.

## September 8, 2020

The following update was made in this release:

**Android Campaign 1.0.6**

* Added support for weak ETags.

## August 3, 2020

The following update was made in this release:

**Android Campaign 1.0.5**

* Added ETag support for Campaign rules download requests.

## April 24, 2020

The following updates were made in this release:

**Android Campaign 1.0.4**

* Changes in how fullscreen in-app messages are displayed inline with WebView security recommendations in Mobile Core 1.5.2 release.
* Report extension details to Mobile Core for improved logging and Griffon support.
* Fixed an image caching related bug, where cached images used to get deleted.

## January 29, 2020

The following updates were made in this release:

**Android Campaign 1.0.3 and iOS Campaign 1.0.5**

* Improved existing log messages and added additional logging to assist with debugging.

## October 28, 2019

The following change was made in this release:

### iOS and Android Campaign Standard 1.1.0

* In the Launch extension, added the ability to reset the `pkey`.

## April 3, 2019

### iOS Campaign Standard 1.0.1

* Fixed an issue with duplicate symbols being present in the Campaign extension library.

