# Troubleshoot Project Griffon

If you are having trouble getting Project Griffon to work, please see suggestions under the following issue topics to resolve commonly encountered issues.

To enable smoother implementation and to discover any potential issues, ensure you have SDK logging turned on per [Enable Debug Logging](https://aep-sdks.gitbook.io/docs/getting-started/enable-debug-logging) in the Getting Started section.

You may change SDK log levels using the [`setLogLevel`](../../foundation-extensions/mobile-core/mobile-core-api-reference.md#logging) API.

## On-device, app issues

### QR code does not open app

* Access the link directly. Copy the link from **Session Details**. Paste it in the browser address bar of the device to open it. If it does not open, please see the section [App will not open link](troubleshoot-project-griffon.md#app-will-not-open-link).
* Use a different QR reader. For iOS 11 or greater, use the Photo app to read the QR code.

### App does not open link

* Verify the deep link implementation is configured correctly in the app.
  * **Android:** Deep Links (App Links)
  * [Create Deep Links to App Context](https://developer.android.com/training/app-links/deep-linking)
* **iOS:** Custom URL Scheme or Universal Links
  * [Defining a Custom URL Scheme for Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
  * [Supporting Universal Links in Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

{% hint style="info" %}
For Android, the`startSession` API does not need to be explicitly called. For iOS, use the API as described in [Adobe Experience Platform Assurance](../../foundation-extensions/adobe-experience-platform-assurance/#implement-aepassurance-session-start-apis-ios-only).
{% endhint %}

### Authentication overlay appears, but app fails to connect

* Ensure internet connectivity of the device through the device web browser.

* If the app has never successfully connected to the Griffon service, ensure it is setup for Project Griffon correctly. See instructions on installing the [Adobe Experience Platform Assurance](../../foundation-extensions/adobe-experience-platform-assurance/#install-the-assurance-extension-in-experience-platform-launch) SDK library.

* Verify the session matches the link and is input correctly for the expected session. See [Log message "OrgID information is not available"](../../foundation-extensions/adobe-experience-platform-assurance/assurance-sdk-error-logs.md#orgid-information-is-not-available) (this is uncommon and relevant only if you have access to more than one ORG instance).

  

### Adobe Analytics Debugging

1. **Post Processing Status - No Debug Flag**

In your Analytics Events view, if your events fail with the Post-Processed Status "No Debug Flag". This is because your current Adobe Analytics or Assurance SDK version might not support the Analytics Debugging feature. 
Please upgrade SDK to the latest version to overcome this problem. Below given are the minimum version requirements.

|                 | iOS     | Android |
| --------------- | ------- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance       | > 1.0.0 | > 1.0.0 |



