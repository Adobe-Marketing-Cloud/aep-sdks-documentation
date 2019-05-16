# Frequently asked questions

## Differences between the Adobe Analytics Mobile SDK v4.x and the Adobe Experience Platform Mobile SDK

One of the main benefits of the Adobe Experience Platform Mobile SDK is the ability to augment functionality by adding solution extensions that do not require an additional SDK.

The table below highlights some of the differneces between the previous generation mobile SDK and the latest Adobe Experience Platform Mobile SDK.

|  | Mobile SDK v4.x | Adobe Experience Platform Mobile SDK |
| :--- | :--- | :--- |


| Programatic Configuration | ✔️ | ✔️ |
| :--- | :--- | :--- |


| SDK Configuration Management | Adobe Mobile Services | Adobe Experience Platform Launch |
| :--- | :--- | :--- |


| Ability to dynamically update configuration |  | ✔️ |
| :--- | :--- | :--- |


| Lifecycle Metrics | ✔️ | ✔️ |
| :--- | :--- | :--- |


| Postback support | ✔️ | ✔️ |
| :--- | :--- | :--- |


| Acquistion links through Adobe Mobile Services | ✔️ | ✔️ |
| :--- | :--- | :--- |


| Push Notifications through Adobe Mobile Services | ✔️ | ✔️ |
| :--- | :--- | :--- |


| In-App Messaging through Adobe Mobile Services | ✔️ | ✔️ |
| :--- | :--- | :--- |


| Adobe Analytics integration | ✔️ | ✔️ Includes the ability to configure separate report suites for dev, stage and production environments |
| :--- | :--- | :--- |


| Adobe Audience Manager integration | ✔️ | ✔️ |
| :--- | :--- | :--- |


| Adobe Campaign Classic support | Requires separate Neolane SDK | ✔️ |
| :--- | :--- | :--- |


| Adobe Campaign Standard |  | ✔️ Includes mobile channel for Push notifications and In-App Messaging |
| :--- | :--- | :--- |


| Adobe Target | ✔️ | ✔️ |
| :--- | :--- | :--- |


| Adobe Target Visual Experience Composer |  | ✔️ |
| :--- | :--- | :--- |


| \(BETA\) Adobe Location Services |  | ✔️ Places Monitor and Location Services extension |
| :--- | :--- | :--- |


| \(BETA\) Project Griffon Mobile Validation |  | ✔️ |
| :--- | :--- | :--- |


| Support for 3rd party vendor extensions |  | ✔️ |
| :--- | :--- | :--- |


### Do I need additional permissions to create a mobile property in Launch?

If you need access to Launch, see this page on [User Permissions](https://docs.adobelaunch.com/launch-reference/administration/user-permissions). If you have permissions to create a web property, you can create a mobile property. If you do not see the option to create a mobile property, turn off your ad blocker, and refresh the page.

### Should I create one property per app or multiple properties per app platform?

If your apps send data to the same Analytics report suites, use the same extensions, rules, data elements, and so on, we recommend that you group all of these mobile apps into the same property. If your apps send data to different Analytics report suites, or user different extensions per app, and so on, we recommend that you create separate mobile properties. Alternatively, if you group your mobile apps into one property, split them into separate properties over time.

### How do I delete a mobile property in Launch?

To delete a mobile property from Launch, see the bottom of [Create a Property](https://docs.adobelaunch.com/getting-started-1/general-launch-configuration-and-settings/create-a-property).

**Warning**: If you delete a mobile property, you cannot undo this action!

## General implementation and migration

### Where can I download the SDK?

The Adobe Experience Platform SDK is available through [Cocoapods](https://cocoapods.org) and [Gradle](https://gradle.org/), and [Github](https://github.com/Adobe-Marketing-Cloud/acp-sdks/). For more information, see [Get the SDK](../../getting-started/get-the-sdk.md).

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

* Mobile Core, which includes Lifecycle, Identity, and Signals frameworks, is required for all other extensions.  The final app size increase can be calculated by adding the Core size to each of the enabled extensions. For example, the iOS app distribution using Target and Analytics will have a total size increase of 635 KB. \(Core: 504 KB + Analytics: 54 KB + Target: 77 KB\).
* iOS \(SDK extension versions 2+\) estimates are based on Xcode’s App Thinning size report for one architecture.  Android \(SDK extension versions 1+\) size estimates listed refer to unsigned apps and do not account for proguarding.

### How can I use ProGuard with the Android SDK?

[Android developer documentation](https://developer.android.com/studio/build/shrink-code) recommends that to make "your APK file as small as possible, you should enable shrinking to remove unused code and resources in your release build". Shrinking is accomplished by using [ProGuard](https://stuff.mit.edu/afs/sipb/project/android/sdk/android-sdk-linux/tools/proguard/docs/index.html#manual/introduction.html).

The Adobe Experience Platform Mobile SDK for Android comes with default ProGuard rules included in the Core `AAR` package \(see `proguard.txt`\). Using this default package is the recommended path of implementation.

If you need to add the following rule to your custom ProGuard rules file - typically labeled as `proguard-rules.pro`. See [Android developer documentation](https://developer.android.com/studio/build/shrink-code#shrink-code) for more information.

```java
-keep class com.adobe.marketing.mobile.* {
    <init>(...);
}
```

## Mobile Core

### What are Lifecycle Metrics?

Lifecycle Metrics are "out-of-the-box" metrics that are automatically collected when the SDK is first implemented in your app. For more information, see [Lifecycle](../../using-mobile-extensions/mobile-core/lifecycle/).

## Adobe Analytics

### How can I setup, configure, or troubleshoot processing rules?

For more information, see [Processing Rules Tips and Tricks](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-tips.html).

### How are mobile visits different from launches?

A launch is measured by the SDK when a user opens the app for the first time or returns to the app after having been out of the app for longer than the specified timeout value. The typical timeout is 5 minutes \(300 seconds\) in [lifecycleTimeout](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle#configuration-keys) configuration setting. A visit is a server-side calculation by Adobe Analytics and is based on the first and last data hits that are sent by the SDK without exceeding a visit timeout. Typically, session timeouts are set at 30 minutes for a report suite. Although visits come from traditional web analytics, these hits still provide valuable insights into how users enter and exit from your app.

### Can I send my analytics data to multiple report suites?

Yes. To capture data in multiple report suites see [Report Suites](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics#report-suites).

