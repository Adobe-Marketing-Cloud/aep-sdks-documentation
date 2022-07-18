# Frequently asked questions

### How can I set up, configure, or troubleshoot processing rules?

To learn about processing rules please read the [processing rules tips and tricks guide](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-tips.html?lang=en).

----

### Why are my Analytics identifiers (AID / MID) changing?

If you see SDK identifiers unexpectedly change, try the following fixes to address the issue. If none of these work, contact Customer Care at your earliest convenience for resolution:

* Ensure that no other versions of the SDK are running - for instance, if you are upgrading SDK versions from 4x to Experience Platform Mobile SDKs - remove all references to 4x SDKs. For 4x SDKs you may look (and remove) for the adobeMobileLibrary/AdobeMobile/AdobeMobileSDK dependency or lib in the project or if the verbose logs indicate ADBMobile prefixed entries.
* Examine app code for logic clearing app user defaults and/or shared preferences. SDK identifiers are stored in app user defaults and shared preferences and may not be cleared for proper functioning of the SDK.
* APIs such as setPrivacyStatus / resetIdentities clear SDK-stored identifiers - ensure that you are appropriately calling these APIs to avoid resetting SDK identifiers.

----

### What identifier types does the AEP Mobile SDK use for Analytics implementations

The Analytics mobile extension uses the ECID as the main identifier type for mobile visitors,and so it requires the Identity extension to operate. The Identity extension preserves the ECID for current visitor, respectively generates a new ECID when the application is first installed. For more details, see the [Identity extension](../../foundation-extensions/mobile-core/identity) documentation.

In the case where your mobile implementation used AID (Analytics tracking identifier) or VID (custom visitor identifier) for existing users, these identifiers are preserved when migrating to AEP Mobile SDK and continue to be sent to Adobe Analytics along with the ECID. Read more about the [order of operations for Analytics IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html).

----

### Why are Crashes inflated in the Analytics report

The metric `Crashes` is computed based on the Lifecycle start and pause API calls implemented in your mobile application. How can you verify if the implementation is correct:

* Ensure that the Lifecycle extension is registered.
* Verify that both MobileCore APIs `lifecycleStart` and `lifecyclePause` are implemented in the application based on the recommended settings for each platform. See the [guide for registering Lifecycle with MobileCore and adding appropriate start/pause calls](../../foundation-extensions/mobile-core/lifecycle).
* For more details, see also [Tracking app crashes in iOS](../../foundation-extensions/mobile-core/lifecycle/lifecycle-extension-in-ios.md#tracking-app-crashes-in-ios) and [Android](../../foundation-extensions/mobile-core/lifecycle/lifecycle-extension-in-android.md#tracking-app-crashes-in-android).

----

### How are mobile visits different from launches?

A launch is measured by the SDK when a user opens the app for the first time or returns to the app after having been out of the app for longer than the specified timeout value. The typical timeout is 5 minutes (300 seconds) in the [lifecycleTimeout](../../foundation-extensions/mobile-core/lifecycle/README.md#configuration-keys) configuration setting.

A visit is a server-side calculation by Adobe Analytics and is based on the first and last data hits that are sent by the SDK without exceeding a visit timeout. Typically, session timeouts are set at 30 minutes for a report suite. Although visits come from traditional web analytics, these hits still provide valuable insights into how users enter and exit from your app.

----

### Can I send my analytics data to multiple report suites?

Yes. To capture data in multiple report suites, please read the [report suites guide](./README.md#report-suites).

----

### I don't see data in my Adobe Analytics report suite - what can I do? <a id="i-dont-see-data-in-my-adobe-analytics-report-suite-what-can-i-do"></a>

If you have followed the documentation and are unable to see reporting data in your Adobe Analytics dashboard, please consider the following next steps:

#### Verify that the Analytics extension is registered

The [Analytics extension](./README.md) and its dependent [Identity extension](../../foundation-extensions/mobile-core/identity/README.md) should be registered and configured correctly for the SDK to start processing trackAction/trackState requests.

#### Verify that network requests are sent to Adobe Analytics <a id="verify-that-network-requests-are-sent-to-adobe-analytics"></a>

You can use [Project Griffon](../../beta/project-griffon/) to verify events are being sent to Adobe Analytics.

#### Ensure appropriate timestamp configuration <a id="ensure-appropriate-time-stamp-configuration"></a>

Ensure that your SDK timestamp configuration is aligned with the report suite's timestamp settings. That is, `analytics.offlineEnabled` in the SDK configuration block for the Launch mobile property is aligned with the setting of Timestamp Configuration in your report suite. You may find Timestamp at Analytics &gt; Admin &gt; Report Suites &gt; General &gt; Timestamp Configuration.

The following settings explain how settings between the SDK and your report suite should be aligned:

* `analytics.offlineEnabled = true` ties to timestamps required or optional
* `analytics.offlineEnabled = false` ties to timestamps not allowed or optional

#### Verify current privacy status

In the mobile property (tag) in the Data Collection UI, select the property from the list, then select **Configure**. If the "Privacy" setting is "Opted Out" the request is dropped by the SDK. If the setting is "Unknown" the request is queued on the device until the status changes to "Opted In" or "Opted Out". If these settings are managed in your app, navigate to the screen where the Privacy settings are updated with the SDK.

#### Contact Adobe Customer Care <a id="contact-adobe-customer-care"></a>

If you are unable to resolve your concerns through resources provided here, please contact [Adobe Experience Cloud customer care](https://experienceleague.adobe.com/?support-solution=General#support) for immediate assistance.
