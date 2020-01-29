# Release Notes

## January 27, 2020

The following updates were made in this release:

**iOS Core 2.4.0**

* Added a new property, `eventUniqueIdentifier`, to the `ACPExtensionEvent` class. 
* Fixed an issue where the advertising identifier was duplicated in the response of the `getSDKIdentifiers` API.
* Fixed an issue where the SDK was trying to download the rules multipile times immediately after app launch.
* Fixed a crash on `std::__1::system_error: mutex lock failed: Invalid argument`.
* Fixed a bug where the iOS fullscreen message was unable to load cached images.



## November 15, 2019

The following updates were made in this release:

### iOS Identity 2.1.3

* Synced custom and advertising identifiers with nil or empty values are now cleared from Identity shared state and local storage. They are also not synced with the Experience Cloud ID \(ECID\) Service.
* Fixed a threading issue where the Experience Cloud ID \(ECID\) Service response was handled on an incorrect thread potentially causing a memory corruption crash.

These changes were released as part of ACPCore CocoaPod v2.3.6.

## October 25, 2019

The following updates were made in this release:

### iOS Core 2.3.5

* Added support for attach data rules consequence.
* Added support for a boolean-type comparison for the Exist or Not Exist rules condition.

### Android Core 1.4.5

* Added support for attach data rules consequence.
* Added support for a boolean-type comparison for the Exist or Not Exist rules condition.
* Fixed a bug where the Exist and Not Exist rules condition might not work for a List or Map type value.
* Fixed a bug that, when fetching the remote config from Launch, might cause a crash on some Android devices.
* Fixed a bug that, when the data URL of an activity did not contain valid schema, might cause a crash.

### Android Identity 1.1.2

* Fixed a bug where the default Experience Cloud Server hostname is now used when no value is configured in the SDK.
* Fixed a bug where multiple custom identifiers with same idType value were synced with the Visitor ID Service.
* Custom visitor identifiers can now be cleared from the SDK by providing a null/empty identifier value for a previously synced idType.

## October 4, 2019

The following updates were made in this release:

### iOS Core 2.3.4

* Fixed a crash that might have happened during app shutdown..    
* Fixed a bug where, when the SDK is being used in multiple threads, the SDK might not function under a race condition..    
* Fixed a bug where the downloaded rules zip file might not be decompressed.    
* Fixed a bug where the getSdkIdentities API used wrong key names for the Push ID and IDFA.    
* Removed the usage of UIWebView.    
* Extension listeners with null/empty type or source is now invalid and will not be registered.    

### iOS Identity 2.1.2

* Fixed an issue where the push identifier is not contained in the Identity shared state on bootup.    
* Fixed an issue where appendToUrl uses the incorrect query delimiter when the source URL contains a question mark in its fragment identifier component.

## September 17, 2019

The following updates were made in this release:

### Android Core 1.4.4

* Starting in API level 16, notifications now support BigTextStyle.
  * This enables long notifications to be displayed without being truncated.
* Fixed the locale string in the HTTP User-Agent to follow the BCP 47 specification.

## September 9, 2019

The following updates were made in this release:

### Android Identity 1.1.1

* Custom identifiers with null or empty IDs are ignored when calling the syncIdentifier or syncIdentifiers APIs because the Visitor ID Service does not support these identifiers.
* The syncIdentifiers API call is ignored when there is an empty Map.
* The duplicate advertising identifier value is removed from the Identity-shared state when MobileCore.setAdvertisingIdentifier is called with a new value.
* The global.ssl configuration settings are ignored, and SSL is enabled by default.
* Fixed an issue where appendVisitorInfoForURL uses the wrong query delimiter when the source URL contains a question mark in its fragment identifier component.

