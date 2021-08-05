# Release Notes

## August 5, 2021

### Android Target 1.2.7

* `TargetRequest` class now provides a constructor with a new `AdobeTargetDetailedCallback`. This callback, when implemented, is invoked with the Target content and a data payload map containing one or more of response tokens, analytics payload and click metric analytics payload, if available in the Target retrieve location content response with or without a prior prefetch call.

**Note**: Adobe Target SDK will continue sending analytics for target payload to Analytics client-side if Adobe Analytics SDK is integrated and registered in the mobile app.

### iOS Target 3.1.0

* `TargetRequest` class now provides a constructor with a new `contentWithDataCallback`. This callback, when implemented, is invoked with the Target content and a data payload map containing one or more of response tokens, analytics payload and click metric analytics payload, if available in the Target retrieve location content response with or without a prior prefetch call.

**Note**: Adobe Target SDK will continue sending analytics for target payload to Analytics client-side if Adobe Analytics SDK is integrated and registered in the mobile app.

* Fixed an issue where the click notification was not being sent to Adobe Target for a retrieved mbox location upon the `clickedLocation` API call.

## June 15, 2021

### Android Target 1.1.7

* Added the changes to move away from bintray and start using Sonatype to push the SDK to Maven Central.

## December 18, 2020

### iOS Target 2.2.0

* The AEP SDKs are now distributed using XCFrameworks in order to support hardware with the new Apple M1 architecture while maintaining support for existing Intel architecture.
  * **IMPORTANT**: Upgrading to XCFrameworks distribution requires Xcode 12.0 or newer
  * **IMPORTANT**: If using Cocoapods, upgrading to the XCFrameworks distribution requires Cocoapods 1.10.0 or newer

## Aug 31, 2020

### iOS Target 2.1.7

* Added support for configuration option `target.server` which enables a custom host to be used for Target requests. This configuration option is available in the Adobe Target Launch extension starting with version 2.4.0.

### Android Target 1.1.6

* Added support for configuration option `target.server` which enables a custom host to be used for Target requests. This configuration option is available in the Adobe Target Launch extension starting with version 2.4.0.
* Public APIs now support error handling via passing `AdobeCallbackWithError`.

## March 11, 2020

The following updates were made in this release:

### Android Target 1.1.5

* Report extension details to Mobile Core for improved logging and Griffon support.
* Target Session Id will now be added as a context data parameter `a.target.sessionId` in the internal Analytics for Target hit sent to Adobe Analytics.
* Fixed an issue, where on app close and relaunch, previously persisted tntId was not being sent in Target requests.

## March 10, 2020

The following updates were made in this release:

### iOS Target 2.1.6

* Report extension details to Mobile Core for improved logging and Griffon support.
* Target Session Id will now be added as a context data parameter `a.target.sessionId` in the internal Analytics for Target hit sent to Adobe Analytics.

## January 29, 2020

The following updates were made in this release:

**Android Target 1.1.4 and iOS Target 2.1.5**

* Improved existing log messages and added additional logging to assist with debugging.

## October 2, 2019

The following updates were made in this release:

### iOS Target 2.1.4

* The Target session ID and Edge Host will now be persisted in `NSUserDefaults`. If there is no activity for the configured `target.sessionTimeout`, these variables will be reset. The default session timeout value is 30 minutes.    

### Android Target 1.1.3

* The Target session ID and Edge Host will now be persisted in Shared Preferences. If there is no activity for the configured `target.sessionTimeout`, these variables will be reset. The default session timeout value is 30 minutes.    
* Fixed an issue where the null `at_property` key, which was passed in mbox parameters, was being sent in Target requests.

## August 8, 2019

The following updates were made in this release:

### iOS Target 2.1.3

* Fixed a bug that, when prefetchContent is called with a nil callback, caused a crash in iOS.

## August 6, 2019

The following updates were made in this release:

### iOS Target 2.1.2 and Android Target 1.1.2

* `target.previewEnabled`, a new configuration Boolean key, has been added. This key is used to enable/disable Target Preview.

  If key is not provided, preview is enabled by default.

* Fixed an issue in Android where Target Preview links were decoded twice, which lead to an error preview page.

## June 27, 2019

The following updates were made in this release:

### iOS Target 2.1.1 and Android Target 1.1.1

* Use the `target.propertyToken` configuration setting to configure the `at_property_token` that is generated from the Target UI, instead of passing the token as an mbox parameter.
* Fixed an issue where JSON offers were not being returned as content but instead default content was served.

## May 15, 2019

### iOS Target 2.1.0 and Android Target 1.1.0

* Upgraded the Target Delivery APIs to latest v1 delivery endpoint.
* Introduced `retrieveLocationContent`, a new API that retrieves content for multiple Target mbox locations simultaneously without increasing the reporting count for prefetch cases.
* Introduced `locationsDisplayed`, a new API that helps Target record location to display events.

  This API should only be used for prefetch scenarios.

* Provided support for `TargetParameters` which is a helper class that combines parameters such as `mboxParameters`, `profileParameters`, `orderParameters`, and `productParameters`.
* New `prefetchContent` and `locationClicked` APIs which accept `TargetParameters`.

## February 28, 2019

The following updates were made to the Adobe Target extension:

The Target Client Code is now automatically added based on your Experience Cloud organization.

* If no code is found, you can type it in.
* If multiple codes are found, you can select the code from the drop-down list.

