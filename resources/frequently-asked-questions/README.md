# Frequently asked questions

## Swift Developer Preview

The Adobe Experience Platform Mobile SDK will soon be available in Swift as an initial, beta release.

[Sign up](https://forms.microsoft.com/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4UJN9zAhIEhJr3PBfyMf9wdUQTI2S0pMVEVYS1k3UUNJVDNDWlRUTFk4Qi4u) for a free developer preview.

## What's new in the Adobe Experience Platform Mobile SDK?

There are several new features and benefits of using the Experience Platform Mobile SDK. These SDKs offer extensions to augment core SDK functionality, server-side configuration, and new Adobe Experience Cloud solution functionality. The following table highlights some of the improvements in the Experience Platform Mobile SDK:

| Core Features | Experience Platform SDK | 4x SDK |
| :--- | :--- | :--- |
| Server-side, dynamic configuration | ✔️ |  |
| Programmatic configuration | ✔️ | ✔️ |
| Configuration UI | [Launch](https://launch.adobe.com) | [Mobile Services](https://mobilemarketing.adobe.com) |
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

### Do I need additional permissions to create a mobile property in Experience Platform Launch?

If you need access to Experience Platform Launch, see [User Permissions](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html). If you create a web property, you can also create a mobile property. If you do not see the option to create a mobile property, turn off your ad blocker, and refresh the page.

### Should I create one property per app or multiple properties per app platform?

If your apps send data to the same Analytics report suites, use the same extensions, rules, data elements, and so on. We recommend that you group all of these mobile apps into the same property. If your apps send data to different Analytics report suites, or user different extensions per app, create separate mobile properties. If you group your mobile apps into one property, you can also split them into separate properties over time.

### How do I delete a mobile property in Experience Platform Launch?

To delete a mobile property from Experience Platform Launch, see [Delete a property](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#delete-a-property).

{% hint style="warning" %}
If you delete a mobile property, you cannot undo this action!
{% endhint %}

## General implementation and migration

### Where can I download the SDK?

The Experience Platform SDK is available through [Cocoapods](https://cocoapods.org) and [Gradle](https://gradle.org/), and [Github](https://github.com/Adobe-Marketing-Cloud/acp-sdks/). For more information, see [Get the SDK](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/0ed8dac3a8db99800c8eda3ada4428f9f1ced6b0/getting-started/get-the-sdk.md).

### Can I use both the 4x SDK and the new Experience Platform SDK at the same time?

Implementing two the SDKs in your app is not recommended, supported, or even technically feasible.

The Experience Platform SDK migrates the locally stored user contexts from the 4x SDKs. Using both SDKs can cause severe data quality issues and user cliffing. For more information, see [Upgrade to the Experience Platform SDKs](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/32dfc7dd49e725872c6daaff6aaaa4535b9d627e/resources/upgrading-to-aep/README.md).

### What platforms are supported?

For a complete list of supported platforms, please see [Latest SDK Versions](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/current-sdk-versions).

### What OS & platform versions are supported?

* Android versions 4.0 or later \(API levels 14 or later\)
* iOS versions 10 or later
* React Native versions 0.44.0 or later
* Flutter versions 1.10.0 or later
* Cordova 9.0.0 or later
* Xamarin - MonoAndroid 9.0+ and Xamarin.iOS 1.0+
* Unity 2019.3.10f1or later

### **Where does the SDK store identities & preferences on the app?**

{% tabs %}
{% tab title="Android" %}
The SDK uses the cache and shared preferences at these locations:

data/data/your.app.package/cache

data/data/your.app.package/shared\_prefs
{% endtab %}

{% tab title="iOS" %}
The SDK uses NSUserDefaults using key prefix Adobe.\*
{% endtab %}
{% endtabs %}

### **How "big" is the SDK?**

| Extension | iOS  \(KB\) | Android \(KB\) |
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

Android developer documentation recommends that to make your APK file as small as possible, enable shrinking to remove unused code and resources in your release build. For more information, see [Shrink, obfuscate, and optimize your app](https://developer.android.com/studio/build/shrink-code). Shrinking is accomplished by using [ProGuard](https://stuff.mit.edu/afs/sipb/project/android/sdk/android-sdk-linux/tools/proguard/docs/index.html#manual/introduction.html). The Experience Platform Mobile SDK for Android comes with default ProGuard rules that are included in the Core `AAR` package \(see `proguard.txt`\). We recommend that you use this default package when you implement.

Add the following rule to your custom ProGuard rules file, typically labeled `proguard-rules.pro`. For more information, see [Shrink, obfuscate, and optimize your app](https://developer.android.com/studio/build/shrink-code).

```java
-keep class com.adobe.marketing.mobile.* {
    <init>(...);
}
```

### How can I track user engagement of push notifications using the Experience Platform Mobile SDK?

How you implement push notification tracking and measurement with the SDK depends on the Experience Cloud solution being used. Specifically, for:

* Adobe Campaign Standard extension, see [Adobe Campaign Standard Push Tracking](https://helpx.adobe.com/campaign/kb/push-tracking.html).
* Adobe Campaign Classic extension, see [Adobe Campaign Classic Push Notifications Tracking](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaignclassic/adobe-campaignclassic-api-reference#tracknotification-api).
* Adobe Analytics - Mobile Services extension, see [Set Up Tracking for Mobile Services Push Notifications](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-push-tracking).

## Mobile Core

### What are Lifecycle metrics?

Lifecycle metrics are out-of-the-box metrics that are automatically collected when the SDK is first implemented in your app. For more information, see [Lifecycle](../../using-mobile-extensions/mobile-core/lifecycle/).

## Adobe Analytics

### How can I set up, configure, or troubleshoot processing rules?

For more information, see [Processing Rules Tips and Tricks](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-tips.html).

### How are mobile visits different from launches?

A launch is measured by the SDK when a user opens the app for the first time or returns to the app after having been out of the app for longer than the specified timeout value. The typical timeout is 5 minutes \(300 seconds\) in [lifecycleTimeout](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle#configuration-keys) configuration setting.

A visit is a server-side calculation by Adobe Analytics and is based on the first and last data hits that are sent by the SDK without exceeding a visit timeout. Typically, session timeouts are set at 30 minutes for a report suite. Although visits come from traditional web analytics, these hits still provide valuable insights into how users enter and exit from your app.

### Can I send my analytics data to multiple report suites?

Yes. To capture data in multiple report suites, see [Report Suites](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics#report-suites).

### I don't see data in my Adobe Analytics report suite - what can I do? <a id="i-dont-see-data-in-my-adobe-analytics-report-suite-what-can-i-do"></a>

If you have followed our documentation and are unable to see reporting data in your Adobe Analytics dashboard, please consider the following next steps:

#### Verify that network requests are sent to Adobe Analytics <a id="verify-that-network-requests-are-sent-to-adobe-analytics"></a>

You may use [Project Griffon](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/32dfc7dd49e725872c6daaff6aaaa4535b9d627e/beta/project-griffon/README.md) to verify events are being sent to Adobe Analytics.

#### Ensure appropriate time-stamp configuration <a id="ensure-appropriate-time-stamp-configuration"></a>

Ensure that your SDK timestamp configuration is aligned with the report suite's time stamp settings. That is, `analytics.offlineEnabled` in the SDK configuration block for the Launch mobile property is aligned with the setting of Timestamp Configuration in your report suite. You may find Timestamp at Analytics &gt; Admin &gt; Report Suites &gt; General &gt; Timestamp Configuration.

The following settings explain how settings between the SDK and your report suite should be aligned:

* `analytics.offlineEnabled = true` ties to Timestamps required or optional
* `analytics.offlineEnabled = false` ties to Timestamps not allowed or optional

#### Contact Adobe Customer Care <a id="contact-adobe-customer-care"></a>

If you are unable to resolve your concerns through resources provided here, please contact [Adobe Experience Cloud customer care](https://helpx.adobe.com/contact/enterprise-support.ec.html) for immediate assistance.

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://helpx.adobe.com/contact/enterprise-support.ec.html) for immediate assistance

