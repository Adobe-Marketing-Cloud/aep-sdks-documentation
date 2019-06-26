# Frequently asked questions

## What's new in the Adobe Experience Platform Mobile SDK?

There are several new features and benefits of using the new Adobe Experience Platform Mobile SDK. The new SDKs offer extensions to augment core SDK functionality, server-side configuration, and new Adobe Experience Cloud solution functionality. The table below highlights some of the improvements made in the  Experience Platform Mobile SDK.

| Core Features | Experience Platform SDK | 4x SDK |
| :--- | :--- | :--- |
| Server-side, dynamic configuration | ✔️ |  |
| Programmatic configuration | ✔️ | ✔️ |
| Configuration UI | [Launch](https://launch.adobe.com) | [Mobile Services](https://mobilemarketing.adobe.com) |
| Partner SDK extensions | ✔️ |  |
| Lifecycle metrics | ✔️ | ✔️ |
| GET/POST postbacks | ✔️ | ✔️ |

| Solution | Experience Platform SDK | 4x SDK |
| :--- | :--- | :--- |
| Adobe Analytics | ✔️ | ✔️ |
| Adobe Analytics - Mobile Services | Messaging and Marketing Links | ✔️ |
| Adobe Audience Manager | ✔️ | ✔️ |
| Adobe Campaign Classic support | ✔️ |  |
| Adobe Campaign Standard | Push and in-app messaging | Push only |
| Adobe Target | ✔️ | ✔️ |
| Adobe Target - Visual Experience Composer | ✔️ | ✔️ |
| \(BETA\) Adobe Experience Platform Location Service | ✔️ |  |
| \(BETA\) Project Griffon Mobile Validation | ✔️ |  |

### Do I need additional permissions to create a mobile property in Experience Platform Launch?

If you need access to Experience Platform Launch, see this page on [User Permissions](https://docs.adobelaunch.com/launch-reference/administration/user-permissions). If you have permissions to create a web property, you can create a mobile property. If you do not see the option to create a mobile property, turn off your ad blocker, and refresh the page.

### Should I create one property per app or multiple properties per app platform?

If your apps send data to the same Analytics report suites, use the same extensions, rules, data elements, and so on, we recommend that you group all of these mobile apps into the same property. If your apps send data to different Analytics report suites, or user different extensions per app, and so on, we recommend that you create separate mobile properties. Alternatively, if you group your mobile apps into one property, split them into separate properties over time.

### How do I delete a mobile property in Experience Platform Launch?

To delete a mobile property from Experience Platform Launch, see the bottom of [Create a Property](https://docs.adobelaunch.com/getting-started-1/general-launch-configuration-and-settings/create-a-property).

**Warning**: If you delete a mobile property, you cannot undo this action!

## General implementation and migration

### Where can I download the SDK?

The Experience Platform SDK is available through [Cocoapods](https://cocoapods.org) and [Gradle](https://gradle.org/), and [Github](https://github.com/Adobe-Marketing-Cloud/acp-sdks/). For more information, see [Get the SDK](../../getting-started/get-the-sdk.md).

### Can I run the 4x SDKs and the new Experience Platform SDKs on my app?

Implementing both SDKs is not recommended or supported.

The Experience Platform SDK migrates the locally stored user contexts from the 4x SDKs. Using both SDKs can cause severe data quality issues and user cliffing. For more information, see [Upgrade to the Experience Platform SDKs](../upgrading-to-aep/).

### **How "big" is the SDK?**

| Extension | iOS  \(KB\) | Android \(KB\) |
| :--- | :--- | :--- |
| Core | 504 | 168 |
| Adobe Analytics | 54 | 21 |
| Adobe Audience Manager | 40 | 13 |
| Adobe Target | 77 | 27 |
| Profile Framework | 20 | 8 |

The size values in the table are provided as indicative estimates, with the following considerations:

* Mobile Core, which includes Lifecycle, Identity, and Signals frameworks, is required for all other extensions.   The final app size increase can be calculated by adding the Core size to each of the enabled extensions. For example, the iOS app distribution using Target and Analytics will have a total size increase of 635 KB. \(Core: 504 KB + Analytics: 54 KB + Target: 77 KB\).
* The iOS \(SDK extension versions 2+\) estimates are based on Xcode’s App Thinning size report for one architecture.   The Android \(SDK extension versions 1+\) size estimates listed refer to unsigned apps and do not account for proguarding.

### How can I use ProGuard with the Android SDK?

[Android developer documentation](https://developer.android.com/studio/build/shrink-code) recommends that _to make your APK file as small as possible, you should enable shrinking to remove unused code and resources in your release build_. Shrinking is accomplished by using [ProGuard](https://stuff.mit.edu/afs/sipb/project/android/sdk/android-sdk-linux/tools/proguard/docs/index.html#manual/introduction.html).

The Experience Platform Mobile SDK for Android comes with default ProGuard rules included in the Core `AAR` package \(see `proguard.txt`\). Using this default package is the recommended path of implementation.

If you need to add the following rule to your custom ProGuard rules file, typically labeled as `proguard-rules.pro`. For more information, see [Android developer documentation](https://developer.android.com/studio/build/shrink-code#shrink-code).

```java
-keep class com.adobe.marketing.mobile.* {
    <init>(...);
}
```

## Mobile Core

### What are Lifecycle Metrics?

Lifecycle Metrics are out-of-the-box metrics that are automatically collected when the SDK is first implemented in your app. For more information, see [Lifecycle](../../using-mobile-extensions/mobile-core/lifecycle/).

## Adobe Analytics

### How can I setup, configure, or troubleshoot processing rules?

For more information, see [Processing Rules Tips and Tricks](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-tips.html).

### How are mobile visits different from launches?

A launch is measured by the SDK when a user opens the app for the first time or returns to the app after having been out of the app for longer than the specified timeout value. The typical timeout is 5 minutes \(300 seconds\) in [lifecycleTimeout](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle#configuration-keys) configuration setting. A visit is a server-side calculation by Adobe Analytics and is based on the first and last data hits that are sent by the SDK without exceeding a visit timeout. Typically, session timeouts are set at 30 minutes for a report suite. Although visits come from traditional web analytics, these hits still provide valuable insights into how users enter and exit from your app.

### Can I send my analytics data to multiple report suites?

Yes. To capture data in multiple report suites, see [Report Suites](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics#report-suites).

