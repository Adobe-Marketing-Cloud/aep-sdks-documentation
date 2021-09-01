# Release Notes

Release notes and change logs for the Adobe Mobile Services extension

## Aug 25, 2021

### iOS AEPMobileServices 3.0.1

* Fixed a bug where shared state was not being read correctly in response to some events.

## Jun 4, 2021

### iOS AEPMobileServices 3.0.0

* Released the brand new Adobe Experience Platform Mobile Services iOS Swift SDK.

## April 14, 2021

### iOS Mobile Services 1.1.1

* Fixed a crash that could happen while downloading remote assets.

## December 18, 2020

### iOS Mobile Services 1.1.0

* The AEP SDKs are now distributed using XCFrameworks in order to support hardware with the new Apple M1 architecture while maintaining support for existing Intel architecture.
  * **IMPORTANT**: Upgrading to XCFrameworks distribution requires Xcode 12.0 or newer
  * **IMPORTANT**: If using Cocoapods, upgrading to the XCFrameworks distribution requires Cocoapods 1.10.0 or newer

## July 31, 2020

### Android Mobile Services 1.0.5

* Fixed an issue where acquisition data may not be correctly processed.

## April 17, 2020

The following updates were made in this release:

### iOS Mobile Services 1.0.6

* Fixed a bug where the modal fullscreen message was shown with a white space at the top of the image.

## February 4, 2020

The following updates were made in this release:

**Android Mobile Services 1.1.1**

* Improved existing log messages and added additional logging to assist with debugging.

## January 23, 2020

The following updates were made in this release:

**iOS Mobile Services 1.0.5**

* The shared state of the Profile extension can now be used as the traits for In-App Messaging.

**Android Mobile Services 1.1.0**

* The shared state of the Profile extension can now be used as the traits for In-App Messaging.
* Added a new API, `MobileServices.processGooglePlayInstallReferrerUrl(final String url)`, to support Google Play Install Referrer APIs.

  For more information about the Install Referrer APIs, see [Still Using InstallBroadcast? Switch to the Play Referrer API by March 1, 2020](https://android-developers.googleblog.com/2019/11/still-using-installbroadcast-switch-to.html).

## November 8, 2019

The following update was made in this release:

**iOS Mobile Servies 1.0.4**

* Fixed a bug where the iOS fullscreen message was unable to load cached images.

## October 7, 2019

The following updates were made in this release:

### iOS Mobile Services 1.0.3

* Full-screen messages now use WKWebViews from the WebKit.framework.
* Local notifications now use the UserNotifications framework.
* Fixed a crash that might happen when the Click-Through or the Cancel button in the Full-screen message was clicked more than once.

## Aug 30, 2019

The following updates were made in this release:

### iOS Mobile Services 1.0.2

* Added the ability to trigger an In-App message that is based on Analytics rules consequences.

### Android Mobile Services 1.0.1

* Added the ability to trigger an In-App message that is based on Analytics rules consequences.

## April 26, 2019

The following updates were made in this release:

### iOS Mobile Services 1.0.1

* Fixed a cocoapod dependency issue.

## April 5, 2019

### iOS Mobile Services 1.0.0

* Mobile Services \(mobilemarketing.adobe.com\) messaging and acquisition links is now supported through the new Mobile Services extension for the Adobe Experience Platform SDK.

