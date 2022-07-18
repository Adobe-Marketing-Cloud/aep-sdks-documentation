# Frequently asked questions

## What's new in the Adobe Experience Platform Mobile SDK?

There are several new features and benefits of using the Experience Platform Mobile SDK. These SDKs offer extensions to augment core SDK functionality, server-side configuration, and new Adobe Experience Cloud solution functionality. The following table highlights some of the improvements in the Experience Platform Mobile SDK:

| Core features | Experience Platform SDK | 4x SDK |
| :--- | :--- | :--- |
| Server-side, dynamic configuration | ✔️ |  |
| Programmatic configuration | ✔️ | ✔️ |
| Configuration UI | [Launch](https://experience.adobe.com/#/data-collection/) | [Mobile Services](https://mobilemarketing.adobe.com) |
| Partner SDK extensions | ✔️ |  |
| Lifecycle metrics | ✔️ | ✔️ |
| GET/POST postbacks | ✔️ | ✔️ |
| Rules & Data Elements | ✔️ |  |

| Solution | Experience Platform SDK | 4x SDK |
| :--- | :--- | :--- |
| Adobe Analytics | ✔️ | ✔️ |
| Adobe Analytics - Media Analytics | ✔️ | ✔️ |
| Adobe Analytics - Mobile Services | Messaging and Marketing Links | ✔️ |
| Adobe Audience Manager | ✔️ | ✔️ |
| Adobe Campaign Classic | ✔️ |  |
| Adobe Campaign Standard | Push and in-app messaging | Push only |
| Adobe Target | ✔️ | ✔️ |
| Places Service | ✔️ |  |
| Project Griffon \(BETA\) | ✔️ |  |

## Do I need additional permissions to create a mobile property in Experience Platform Launch?

If you need access to Experience Platform Launch, see the [user permissions document](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=en). If you create a web property, you can also create a mobile property. If you do not see the option to create a mobile property, turn off your ad blocker, and refresh the page.

## Should I create one property per app or multiple properties per app platform?

If your apps send data to the same Adobe Analytics report suites, use the same extensions, rules, and data elements. You should group all of these mobile apps into the same property. If your apps send data to different Adobe Analytics report suites or user different extensions per app, create separate mobile properties. If you group your mobile apps into one property, you can also split them into separate properties over time.

## How do I delete a mobile property in Adobe Experience Platform Launch?

To delete a mobile property from Adobe Experience Platform Launch, please read the [delete a property tutorial](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#delete-a-property).

{% hint style="warning" %}
If you delete a mobile property, you cannot undo this action!
{% endhint %}

## General implementation and migration

### Where can I download the SDK?

The Experience Platform SDK is available through [Cocoapods](https://cocoapods.org) and [Gradle](https://gradle.org/), and [Github](https://github.com/Adobe-Marketing-Cloud/acp-sdks/). For more information, please read the [get the SDK tutorial](../../getting-started/get-the-sdk.md).

### Can I use both the 4x SDK and the new Experience Platform SDK at the same time?

Implementing two the SDKs in your app is not supported.

The Experience Platform SDK migrates the locally stored user contexts from the 4x SDKs. Using both SDKs will cause severe data quality issues. For more information, please read the [upgrade to the Experience Platform SDKs tutorial](../upgrading-to-aep/).

### What platforms are supported?

For a complete list of supported platforms, please read the [latest SDK versions document](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions).

### What OS and platform versions are supported?

* Android versions 4.0 or later \(API levels 14 or later\)
* iOS versions 10 or later
* React Native versions 0.44.0 or later
* Flutter versions 1.10.0 or later
* Cordova 9.0.0 or later
* Xamarin - MonoAndroid 9.0+ and Xamarin.iOS 1.0+
* Unity 2019.3.10f1or later

### Where does the SDK store identities and preferences on the app?

{% tabs %}
{% tab title="Android" %}
The SDK uses the cache and shared preferences at these locations:

data/data/your.app.package/cache

data/data/your.app.package/shared\_prefs
{% endtab %}

{% tab title="iOS" %}
The SDK uses `NSUserDefaults` using the prefix `adobe.*`.
{% endtab %}
{% endtabs %}

### What is the size of the SDK?

| Extension | iOS \(KB\) | Android \(KB\) |
| :--- | :--- | :--- |
| Core | 504 | 168 |
| Adobe Analytics | 54 | 21 |
| Adobe Audience Manager | 40 | 13 |
| Adobe Target | 77 | 27 |
| Profile | 20 | 8 |
| Adobe Campaign Standard | 60 | 30 |
| Places | 36 | 20 |
| Places Monitor | 10 | 19 |

The size values in the table are provided as indicative estimates, with the following considerations:

* Mobile Core, which includes the Lifecycle, the Identity, and the Signals extensions, is required for all other extensions. The final app size increase can be calculated by adding the Mobile Core size to each of the enabled extensions. For example, the iOS app distribution using the Target and Analytics extensions will have a total size increase of 635 KB. \(Core: 504 KB + Analytics: 54 KB + Target: 77 KB\).
* The iOS \(SDK extension versions 2+\) estimates are based on Xcode’s App Thinning size report for one architecture. The Android \(SDK extension versions 1+\) size estimates listed refer to unsigned apps and do not account for proguarding.

### How can I use ProGuard with the Android SDK?

Android developer documentation recommends that you should enable shrinking to remove unused code and resources in your release build to make your APK file as small as possible. For more information, please read the [shrink, obfuscate, and optimize your app tutorial](https://developer.android.com/studio/build/shrink-code). Shrinking is accomplished by using [ProGuard](https://stuff.mit.edu/afs/sipb/project/android/sdk/android-sdk-linux/tools/proguard/docs/index.html#manual/introduction.html). The Experience Platform Mobile SDK for Android comes with default ProGuard rules that are included in the Core `AAR` package \(see `proguard.txt`\). You should use this default package when you implement.

Add the following rule to your custom ProGuard rules file, typically labeled `proguard-rules.pro`. For more information, please read the [shrink, obfuscate, and optimize your app tutorial](https://developer.android.com/studio/build/shrink-code).

```java
-keep class com.adobe.marketing.mobile.* {
    <init>(...);
}
```

### How can I track user engagement of push notifications using the Experience Platform Mobile SDK?

Implementing push notification tracking and measurement with the SDK depends on the Experience Cloud solution being used.

* For the Adobe Campaign Standard extension, please read the [Adobe Campaign standard push tracking tutorial](https://experienceleague.adobe.com/docs/campaign-standard/using/administrating/configuring-mobile/push-tracking.html?lang=en).
* For the Adobe Campaign Classic extension, please read the [Adobe Campaign Classic push notifications tracking tutorial](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaignclassic/adobe-campaignclassic-api-reference#tracknotification-api).
* For the Adobe Analytics - Mobile Services extension, please read the [set up tracking for Mobile Services push notifications tutorial](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-push-tracking).

## Mobile Core

### What are Lifecycle metrics?

Lifecycle metrics are out-of-the-box metrics that are automatically collected when the SDK is first implemented in your app. For more information, please read the [documentation on Lifecycle metrics](../../foundation-extensions/mobile-core/lifecycle/).

## Adobe Analytics

See the [frequently asked questions for Analytics](../../using-mobile-extensions/adobe-analytics/analytics-faq.md).

## Adobe Experience Platform Edge Network

### Does AEP Edge Network extension support offline tracking?

Yes, offline tracking is supported by default when sending XDM Experience events since these events have a required timestamp, and there is no separate setting for this as it used to be in the Adobe Analytics extension. The events are backed up in the persistence layer and then sent to the Edge Network in current session if possible, or queued until the next session when a network connection is available.

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://experienceleague.adobe.com/?support-solution=General#support) for immediate assistance

## Using AEP Swift SDKs with tvOS

### 'X' is unavailable in application extension for tvOS

You may encounter this error when using the AEP SDK for a tvOS app target, with the following message "'X' is unavailable in application extension for tvOS". This behavior is unexpected for tvOS targets and it seems to be an issue in Xcode where it apples additional checks for tvOSApplicationExtension API compatibility.
Until this issue is resolved in the future Xcode versions, a workaround is to mark the classes or functions with the attribute: @available(tvOSApplicationExtension, unavailable) to suppress the error as in the examples below:

#### Sample
```Swift
@available(tvOSApplicationExtension, unavailable)
class ErrorThrowingClass {
  ...
}
```

```Swift
@available(tvOSApplicationExtension, unavailable)
func errorThrowingFunction() {
  ...
}
```
