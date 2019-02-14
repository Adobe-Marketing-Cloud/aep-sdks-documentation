# Frequently asked questions

### Launch

#### Do I need additional permissions to create a mobile property in Launch?

If you need access to Launch, see this page on [User Permissions](https://docs.adobelaunch.com/administration/user-permissions). If you have permissions to create a web property, you're all setup to create a mobile property. If you don't see the option to create a mobile property - you may refresh the page with your ad-blocker turned off.

#### Should I create one property per app or multiple properties per app platform?

If your apps send data to the same Analytics report suites, use the same extensions, rules, data elements, etc. - we recommend you group all of these mobile apps into the same property. If your apps send data to different Analytics report suites, or user different extensions per app, etc. then we suggest creating separate mobile properties. Alternatively, if you group your mobile apps into a single property, you should be able easily to split them out into separate properties over time.

#### How to delete a mobile property in Launch?

You may delete a mobile property from Launch by following these [instructions](https://docs.adobelaunch.com/administration/companies-and-properties#delete-a-property). Please note that if you choose to delete a mobile property, it may not be undone.

### General Implementation & Migration

#### Where can I download the SDK?

The Adobe Experience Platform SDK is available via [Cocoapods](https://cocoapods.org) and [Gradle](https://gradle.org/) - see [Get the SDK](../getting-started/get-the-sdk.md). It is also available on [Github](https://github.com/Adobe-Marketing-Cloud/acp-sdks/).

#### Can I run both 4x and the new Adobe Experience Platform SDKs on my app?

Implementing both SDKs is not recommended or supported. The Experience Platform SDK migrates 4x SDK's locally stored, user context. Using both SDKs can cause severe data quality issues and user cliffing. See the [upgrade](upgrading-to-aep/) guide for more information.

#### **How "big" is the SDK?**

| Extension | iOS  \(KB\) | Android \(KB\) |
| :--- | :--- | :--- |
| Core | 504 | 168 |
| Adobe Analytics | 54 | 21 |
| Adobe Audience Manager | 40 | 13 |
| Adobe Target | 77 | 27 |
| Profile Framework | 20 | 8 |

Please note that the size figures listed above are provided as indicative estimates, with the following considerations:

* Core \(includes Lifecycle, Identity, and Signals frameworks\) is required for all other extensions, so final app size increase can be calculated by adding Core size to each of the enabled extensions. For example: iOS app distribution using Target and Analytics would have a total size increase of 635 KB \(Core: 504 KB + Analytics: 54 KB + Target: 77 KB\).
* iOS \(SDK extension versions 2+\) estimates are based on Xcode’s App Thinning size report for a single architecture. Android \(SDK extension versions 1+\) size estimates listed refer to unsigned apps and do not account for proguarding.

### Mobile Core

#### What are Lifecycle Metrics?

Lifecycle Metrics are "out-of-the-box" metrics that are automatically collected when the SDK is first implemented in your app. For more information, see [Lifecycle](../using-mobile-extensions/mobile-core/lifecycle/).

### Adobe Analytics

#### How can I setup, configure, or troubleshoot processing rules?

For more information, see [Processing Rules Tips and Tricks](https://marketing.adobe.com/resources/help/en_US/reference/processing_rules_tips.html).

#### How are mobile visits different from launches?

A launch is measured by the SDK when a user opens the app for the first time or returns to the app after having been out of the app for longer than the specified timeout value. The typical timeout is 5 minutes \(300 seconds\) in [lifecycleTimeout](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle#configuration-keys) configuration setting. A visit is a server-side calculation by Adobe Analytics and is based on the first and last data hits that are sent by the SDK without exceeding a visit timeout. Typically, session timeouts are set at 30 minutes for a report suite. Although visits come from traditional web analytics, these hits still provide valuable insights into how users enter and exit from your app.

#### Can I send my analytics data to multiple report suites?

Yes. To capture data in multiple report suites see [Report Suites](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics#report-suites).

