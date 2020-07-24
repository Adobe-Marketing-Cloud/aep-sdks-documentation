# Troubleshoot Project Griffon

If you are having trouble getting Project Griffon to work, please see suggestions under the following issue topics to resolve commonly encountered issues.

To enable smoother implementation and to discover any potential issues, ensure you have SDK logging turned on per [Enable Debug Logging](https://aep-sdks.gitbook.io/docs/getting-started/enable-debug-logging) in the Getting Started section.

You may change SDK log levels using the [`setLogLevel`](../../using-mobile-extensions/mobile-core/mobile-core-api-reference.md#logging) API.

## On-device, app issues

### QR code does not open app

* Access the link directly. Copy the link from **Session Details**. Paste it in the browser address bar of the device to open it. If it does not open, please see the section [App will not open link](troubleshoot-project-griffon.md#app-will-not-open-link).
* Use a different QR reader. For iOS 11 or greater, use the Photo app to read the QR code.

### App does not open link

* Verify the deep link implementation is configured correctly in the app.
  * **Android:** Deep Links \(App Links\)
  * [Create Deep Links to App Context](https://developer.android.com/training/app-links/deep-linking)
* **iOS:** Custom URL Scheme or Universal Links
  * [Defining a Custom URL Scheme for Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
  * [Supporting Universal Links in Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

{% hint style="info" %}
For Android, the`startSession` API does not need to be explicitly called. For iOS, use the API as described in [Set up Project Griffon ](set-up-project-griffon/#startsession).
{% endhint %}

### Authentication overlay appears, but app fails to connect

* Ensure internet connectivity of the device through the device web browser.
* If the app has never successfully connected to the Griffon service, ensure it is setup for Project Griffon correctly. See [Set up Project Griffon](set-up-project-griffon/).
* Verify the session matches the link and is input correctly for the expected session. See [Log message "OrgID information is not available"](troubleshoot-project-griffon.md#sdk-log-message-orgid-information-is-not-available) \(this is uncommon and relevant only if you have access to more than one ORG instance\).

## SDK error logs

### OrgID information is not available

* Verify the AppID is correct in the Mobile Core `configureWithAppID` method.
* Make sure you have published the configuration with [Experience Platform Launch](https://launch.adobe.com/). See [Publish the configuration](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property#publish-the-configuration).

Sample SDK log messages:

```text
(Android) E/AdobeExperienceSDK: Griffon - Org id is null or empty
(Android) D/AdobeExperienceSDK: Griffon - Unable to start griffon session experience cloud OrgID is not available. Verify if the MobileCore is aptly configured.

(iOS) ERROR <ACPGriffon>]: Unable to start griffon session experience cloud OrgID is not available. Verify if the ACPCore is aptly configured.
```

### Timeout

* This log message is not a problem by itself. It is expected if the app was not launched with a Griffon deep link. You may ignore this error if Project Griffon works as expected.

Sample log messages:

```text
(Android) D/AdobeExperienceSDK: Griffon - Timeout - Griffon did not receive deeplink to start griffon session within 5 seconds. Shutting down griffon extension

(iOS) [AdobeExperienceSDK DEBUG <ACPGriffon>]: Timeout - Griffon didnot receive deeplink to start griffon session. Shutting down griffon extension
```

### Failed to show fullscreen takeover

* This log message is not a problem and will appear with typical usage. You may ignore this error if Project Griffon works as expected.

Sample log message:

```text
(Android) E/AdobeExperienceSDK: Griffon - Failed to show fullscreen takeover, could not get fullScreenTakeover object.
```

