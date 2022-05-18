# Release Notes

## May 18, 2022

### Android Campaign Classic 1.0.2

* Android Campaign Classic SDK is now Adobe Campaign Classic (ACC) v8 compatible! Broadlog ID can be provided in the UUID format in the notification tracking APIs.

## May 17, 2022

### iOS Campaign Classic 2.1.1

* ACPCampaignClassic iOS SDK is now Adobe Campaign Classic (ACC) v8 compatible! Broadlog ID can be provided in the UUID format in the notification tracking APIs.

## December 18, 2020

### iOS Campaign Classic 2.1.0

* The AEP SDKs are now distributed using XCFrameworks in order to support hardware with the new Apple M1 architecture while maintaining support for existing Intel architecture.
  * **IMPORTANT**: Upgrading to XCFrameworks distribution requires Xcode 12.0 or newer
  * **IMPORTANT**: If using Cocoapods, upgrading to the XCFrameworks distribution requires Cocoapods 1.10.0 or newer

## March 19, 2020

The following updates were made in this release:

### Android Campaign Classic 1.0.1

* Report extension details to Mobile Core for improved logging and Griffon support.
* Fixed a security issue where hex conversion method was vulnerable to hash collisions.

## March 18, 2020

The following updates were made in this release:

### iOS Campaign Classic 2.0.3

* Report extension details to Mobile Core for improved logging and Griffon support.
* Fixed an issue where passing nil callback in `registerDevice` API caused a crash.

## October 10, 2019

The following updates were made in this release:

### iOS Campaign Classic 2.0.1

* Fixed an issue where, on iOS 13, the push token was not being extracted correctly from NSData during device registration.
* Fixed an issue where the charset information was not being sent in the Content-Type header during device registration call.

