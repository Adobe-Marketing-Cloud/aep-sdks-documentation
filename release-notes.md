# Release notes

## April 16, 2019

Project Griffon is now available for beta access!

Project Griffon is a new, innovative product from Adobe to help you easily inspect, validate, debug data collection and experiences for your mobile app. Developed for app product managers and developers, Project Griffon ensures that your app is correctly implemented, which allows you to focus on creating engaging experiences.

Project Griffon is in beta, and the use of this beta release requires you to accept the terms outlined in [https://griffon.adobe.com](https://griffon.adobe.com).

If you need access, go to [https://griffon.adobe.com](https://griffon.adobe.com) and [register your interest](https://forms.office.com/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4UJN9zAhIEhJr3PBfyMf9wdUMjNHTjVCVUJXUDM0VUIzOUFWMk9RNlBLRC4u).

To learn more about Project Griffon, here are the links to the documentation:

* [Set up Project Griffon](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/fd6137a4ad0388193660ec6714c735650d6f885d/set-up-project-griffon.md)
* [Using Project Griffon](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/fd6137a4ad0388193660ec6714c735650d6f885d/using-project-griffon.md)

## April 9, 2019

The ACPlaces Monitor version 1.0.1 is now available!

Here are the changes in this release:

* Added full unit test coverage.
* CI integration \(CircleCI\)
* Code coverage integration \(codecov\)

## April 5, 2019

iOS Core 2.1.1 release: 

* Core: Internal support for database scheme migration. 
* Identity:  Identity MID might be regenerated when privacy settings change from opted out to opted in/opt unknown in the same session. 

iOS Analytics 2.0.3 release: 

* Fixed a minor Analytics hit ordering issue. 

iOS Mobile Services 1.0.0 release: 

* Mobile Services \(mobilemarketing.adobe.com\) messaging and acquisition links is now supported through the new Mobile Services extension for the Adobe Experience Platform SDK.

## April 3, 2019

The Adobe Campaign Standard extension version 1.0.1 is now available for iOS.

This update fixed an issue with duplicate symbols being present in the Campaign extension library.

## March 25, 2019

The following update was made to the Mobile Core extension in iOS version 2.1.0:

### Configuration

If there is no cached configuration available, the SDK can fetch the configuration after a network restore.

### Core

* Added the `ACPCore` log API, which allows third-party extensions and application developers to log messages and use the Mobile SDK `LogLevel` to select the verbosity of the logs.
* You can also use the ACPCore `getLogLevel` API to retrieve the current `LogLevel` that was set in the SDK.
* `trackAction` and `trackState` only accept `NSDictionary`-type context data.

## March 21, 2019

The Adobe Campaign Standard extension version 1.0.0 is now available for Android!

This extension allows you to deliver and track in-app messages \(broadcast and personalized\) and push notifications to mobile app users from Adobe Campaign Standard.

## March 21, 2019

The following update was made to the Mobile Core extension in Android version 1.2.1:

* Added protection around null results when `toString` is called on Intent extras data.

## March 20, 2019

The following update was made to the Mobile Core extension in Android version 1.2.0:

### **Configuration**

* If there is no cached configuration available, you can fetch the configuration after a network restore.
* Added environment-aware support, which allows you to define dev and stage environments in a property. \_\*\*\_This overrides the config properties that were based on the default environment.

### Core

* Added the `MobileCore.getApplication` API, which allows third-party extension developers access the application context.
* Added the `MobileCore.log` API, which allows third-party extensions and application developers to log messages and use the Mobile SDK `LoggingMode` to select the verbosity of the logs.
* You can also use the `MobileCore.getLogLevel` API to retrieve the current `LoggingMode` that was set in the SDK.

### Identity

* You can regenerate the MID when privacy settings change from opted out to opted in/opt unknown in the same session.

## March 14, 2019

The following update was made to the Mobile Core extension in Android version 1.1.2:

* Resolved an issue that might result in a crash when the underlying Analytics database was corrupted.

## March 7, 2019

The following update was made to the Mobile Core extension in Android version 1.1.1:

* Resolved an issue that could result in a crash when the underlying Analytics database was corrupted.

## March 1, 2019

The following update was made to the Mobile Core extension in Android version 1.1.0:

* The `setSmallIcon` and `setLargeIcon` APIs were added.

The following update was made to the Mobile Analytics extension in Android version 1.1.1:

* Use the `analytics.launchHitDelay` configuration setting to indicate how long to wait before Analytics launch hits are sent.

## February 28, 2019

The first version of Places is now available for public beta access!

The Places solution is composed of the following components:

* The **Places Services** is a robust set of REST APIs that provide an interface to the database that stores all Places-related data for a customer.  For more information, see [Places database management](https://launch.gitbook.io/places-services-by-adobe-documentation/places-database-management-1). 
* A **Places-specific card** on Adobe IO \(coming soon\). 
* The **Places UI** is built on the APIs that are provided by the Places Service and allows customers to create and manage their Places libraries.

  To log in to the Places UI, go to [https://places.adobe.com](https://places.adobe.com).

* The **Places Extension \(Launch & SDK\)** The functionality in the extension retrieves the relevant Places data from the Places Services based on the location of the calling device. The SDK extension also dispatches Places-related events on the Event Hub for consumption by the Rules Engine and other interested extensions:
  * **GitHub**: [https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/tag/v1.0.0-ACPPlaces](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/tag/v1.0.0-ACPPlaces) 
  * **Cocoapod**: [https://cocoapods.org/pods/ACPPlaces](https://cocoapods.org/pods/ACPPlaces) 
  * **Maven Central**: [https://mvnrepository.com/artifact/com.adobe.marketing.mobile/places](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/places)

### Documentation Links

To learn more about Places, here are links to the documentation:

* UI - [https://launch.gitbook.io/places-services-by-adobe-documentation/](https://launch.gitbook.io/places-services-by-adobe-documentation/)
* SDK - [https://aep-sdks.gitbook.io/docs/using-mobile-extensions/places-extension](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/places-extension)

## February 28, 2019

The Target extension has been enhanced.

The Target Client Code is now automatically added based on your Experience Cloud organization.

* If no code is found, you can type it in.
* If multiple codes are found, you can select the code from the drop-down list.

## February 20, 2019

The Adobe Campaign Standard extension version 1.0.0 is now available!

This extension allows you to deliver and track in-app messages \(broadcast and personalized\) and push notifications to mobile app users from Adobe Campaign Standard.

## February 19, 2019

The following updates were made to the Mobile Core extension in iOS version 2.0.3:

* Bug fixes

## February 7, 2109

The following updates were made to the Mobile Core extension in iOS version 2.0.2:

* Resolved an issue that caused failures when retrieving a configuration on application launch.

## January 24, 2019

The January 24th update includes changes to the Adobe Experience Platform Mobile SDKs and solution extensions for iOS applications. We provided an explanation of this change, why the changes were made, and how to update your application to include these changes.

### What

With this release, we have changed the Mobile SDK Core and all Adobe solution extensions from dynamic frameworks to static libraries.

### Why

Frameworks are an excellent way to package and distribute iOS dependencies but, in some situations, using frameworks can cause issues when a dependent framework is updated. All of the Adobe Experience Platform SDK extensions have a dependency on the Core extension. This means that when a change is made to the Mobile Core framework, all dependent extensions need to be rebuilt from the source. To resolve this issue, we changed the SDK Core and all Adobe solution extensions to use static libraries.

### How

There is nothing wrong or broken with the previous versions of the SDK. Apps that have already started development with the version 1.x SDK and extensions can continue in the development lifecycle with no impact. Mobile applications that have not yet started to implement the Mobile SDKs are also fine, as they will start out using the static libraries. The changes listed below are required for customers who have started implementing the Adobe Experience Platform Mobile SDK and want to update to the latest version.

{% hint style="info" %}
The changes are only for iOS.
{% endhint %}

To update existing Experience Platform Mobile SDK 1.x implementations to 2.x:

1. Use the latest installation instructions for your selected environment \(development, staging, production\).
2. Update your Pod file with the latest changes.
3. Run a 'pod update' command to pull in the latest version of the Mobile Core extension and any other solution extension updates.
4. In your app code, change all of your import statements:  

**For Objective-C**

Where you previously had imports that look like the following:

```text
   #import <ACPCore_iOS/ACPCore_iOS.h> 
   #import <ACPIdentity_iOS/ACPIdentity_iOS.h> 
   #import <ACPLifecycle_iOS/ACPLifecycle_iOS.h>
   #import <ACPSignal_iOS/ACPSignal_iOS.h>
   #import <ACPUserProfile_iOS/ACPUserProfile_iOS.h>
```

The imports will now drop the _iOS_ suffix and can be imported directly as follows:

```text
   #import "ACPCore.h" 
   #import "ACPIdentity.h" 
   #import "ACPLifecycle.h" 
   #import "ACPSignal.h" 
   #import "ACPUserProfile.h"
```

This change will hold true for any other Adobe solution extensions that you may have previously imported.

**For Swift**

Where you previously had imports that looked like:

```swift
   import ACPCore_iOS
   import ACPAnalytics_iOS
   import ACPIdentity_iOS
   import ACPLifecycle_iOS
   import ACPSignal_iOS
   import ACPUserProfile_iOS
```

The imports will now drop the _iOS_ suffix. Additionally, the Identity, Lifecycle and Signals extensions can be added just by importing core , for example:

```swift
    import ACPCore
    import ACPAnalytics
    import ACPUserProfile
```

We feel that this update will serve our customers and partners better in the long run. If you have any questions or issues, go to our [user forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk#).

## December 5, 2018

The following updates were made to the Mobile Core extension in iOS version 1.1.1:

* Fixed a bug where the `deviceToken` conversion was incorrect in some situations.

## December 4, 2018

The following updates were made to all extensions:

**iOS version 1.1.0**

* All ACP frameworks now properly run on 32-bit devices.

## November 30, 2018

The following changes were made to the Mobile Core extension in iOS version 1.0.2:

* Minor bug fixes

## November 20, 2018

The Adobe Campaign Classic extension version 1.0.0 is now available!

This extension enables the delivery and tracking of push notifications to mobile app users from Adobe Campaign Classic.

{% hint style="info" %}
This extension is only for Adobe Campaign Classic and will not work with Adobe Campaign Standard.
{% endhint %}

#### Key Features

In this release, you can:

* Send push tokens with information about the user and the device to Adobe Campaign Classic so that users can enable push messaging to mobile app users who opt in to notifications.
* Send additional custom profile data to Adobe Campaign Classic, which allows personalized push notifications.
* Track the receipt of push messages \(impressions\) in Android apps and silent notifications in iOS apps.
* Track when users click on push notifications.

Here is some additional information:

This extension is an alternative to the stand-alone Campaign Classic SDK. It allows Experience Platform SDK users to enable push messaging from Campaign Classic without installing the Campaign Classic SDK separately.

## November 16, 2018

The following updates were made to the Mobile Core extension:

**iOS version 1.0.1**

* Fixed a bug for extensions where the response callback was not called for the `dispatchEventWithResponseCallback` API.
* Minor bug fixes.

**Android version 1.0.5**

* This version now includes the _proguard-rules.pro_ config file.
* Minor bug fixes.

## September 27, 2018

### Adobe Experience Platform SDKs are live!

* Version 1.0.0 of the Experience Platform SDKs were released for the Mobile Core, Analytics, Audience Manager, and Adobe Target extensions.

