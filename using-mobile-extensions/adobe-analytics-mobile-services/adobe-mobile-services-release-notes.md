# Release Notes

Release notes and change logs for the Adobe Mobile Services extension

## November 5, 2021

 ### iOS AEPMobileServices 3.0.3

 * Fixes crash when using an immutable dictionary for handling attribution data.

## Oct 18, 2021

 ### iOS AEPMobileServices 3.0.2

 * Includes deferred link info to Acquisition response event when available.

## Oct 05, 2021

### Android MobileServices 1.1.5

* Specifies mutability of each PendingIntent object that the SDK creates [for Android 12 changes](https://developer.android.com/about/versions/12/behavior-changes-12#pending-intent-mutability) 

## Aug 25, 2021

### iOS AEPMobileServices 3.0.1

* Fixed a bug where shared state was not being read correctly in response to some events.

## Jun 4, 2021

### iOS AEPMobileServices 3.0.0

* Released the brand new Adobe Experience Platform Mobile Services iOS Swift SDK.

## July 31, 2020

### Android Mobile Services 1.0.5

* Fixed an issue where acquisition data may not be correctly processed.

## February 4, 2020

The following updates were made in this release:

### Android Mobile Services 1.1.1

* Improved existing log messages and added additional logging to assist with debugging.

## January 23, 2020

The following updates were made in this release:

### Android Mobile Services 1.1.0

* The shared state of the Profile extension can now be used as the traits for In-App Messaging.
* Added a new API, `MobileServices.processGooglePlayInstallReferrerUrl(final String url)`, to support Google Play Install Referrer APIs.

  For more information about the Install Referrer APIs, see [Still Using InstallBroadcast? Switch to the Play Referrer API by March 1, 2020](https://android-developers.googleblog.com/2019/11/still-using-installbroadcast-switch-to.html).

## Aug 30, 2019

The following updates were made in this release:

### Android Mobile Services 1.0.1

* Added the ability to trigger an In-App message that is based on Analytics rules consequences.
