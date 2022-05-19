# Release Notes

## May 18, 2022

### iOS AEPAudience 3.0.4

* Fixed an issue where lifecycle data was included in signalWithData requests.

## May 9, 2022

### iOS AEPAudience 3.0.3

- Fixed integration with Lifecycle extension to send lifecycle metrics when a new app session is started.

## Jul 13, 2021

### iOS AEPAudience 3.0.2

* Added support to handle the MobileCore.resetIdentities\(\) API.

## April 1, 2021

### iOS AEPAudience 3.0.1

* Updated syncedVisitorIds implementation to a map
* Fixed access modifer for two classes

## January 29, 2021

### iOS Audience 3.0.0

* Initial release to support [Adobe Audience](./)  for Adobe Experience Platform Mobile SDKs for iOS in Swift. This extension library is available as an [open sourced project on Github](https://github.com/adobe/aepsdk-audience-ios/).

## January 20, 2021

### iOS Audience 2.3.0

* Added tvOS compatibility

## December 18, 2020

### iOS Audience 2.2.0

* The AEP SDKs are now distributed using XCFrameworks in order to support hardware with the new Apple M1 architecture while maintaining support for existing Intel architecture.
  * **IMPORTANT**: Upgrading to XCFrameworks distribution requires Xcode 12.0 or newer
  * **IMPORTANT**: If using Cocoapods, upgrading to the XCFrameworks distribution requires Cocoapods 1.10.0 or newer

## November 9, 2020

### iOS Audience 2.1.0

* Added new APIs getVisitorProfileWithCompletionHandler, signalWithData:WithCompletionHandler. These APIs take completion handler as an argument which is invoked with the desirable response or an NSError if an unexpected error occurs or the request times out.
* Added changes to publish Audience shared state on EventHub boot.
* Fixed an issue to handle Analytics response only if AAMForwarding is enabled.

### Android Audience 1.1.0

* Added support for AdobeCallbackWithError for APIs getVisitorProfile, signalWithData.
* Added changes to publish Audience shared state on EventHub boot.

## July 17, 2020

### Android Audience 1.0.2

* Fixed an issue where UUID was not returned in getSdkIdentities API response.
* Fixed an issue where customer visitor IDs were missing from Audience signals.

### @adobe/react-native-acpaudience@1.1.2

* Updated to iOS Audience 2.0.2.
* Updated to Android Audience 1.0.2.

## July 10, 2020

### iOS Audience 2.0.2

* Fixed an issue where UUID was not returned in getSdkIdentities API response.

## September 24, 2019

The following change was made in this release:

### iOS Audience 2.0.1

* The `global.ssl` configuration settings are ignored, and SSL is enabled by default.
* Appends IMS OrgID to AAM demdex calls if subdomain endpoint is missing.

