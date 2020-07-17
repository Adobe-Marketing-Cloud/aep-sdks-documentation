# Troubleshoot Project Griffon



## Enable debug logging

Change the log level with MobileCore/ACPCore  `setLogLevel` API. See [Enable Debug Logging](https://aep-sdks.gitbook.io/docs/getting-started/enable-debug-logging).



## QR does not open app

Use a different QR reader. For iOS 11 or greater, use the Photo app to read the QR code.  

Access the link directly. Copy the link from **Session Details**. Paste it in the browser address bar of the device and try to open it. If it does not open, please see the section [App will not open link](#app-will-not-open-link).



## App will not open link

Verify the deep link implementation is configured correctly in the app. 

**Android:** Deep Links (App Links)

- [Create Deep Links to App Contect](https://developer.android.com/training/app-links/deep-linking)

**iOS:** Custom URL Scheme or Universal Links

- [Defining a Custom URL Scheme for Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
- [Supporting Universal Links in Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

For Android, the `startSession` API does not need to be explicity called. For iOS, call the API from the correct place as describe in [Set up Project Griffon ](../set-up-project-griffon#startsession).



## PIN authentication overlay appears, but the app fails to connect to the Griffon service

Check internet connectivity of the device through a web browser.

If the app has never successfully connected to the Griffon service, check that it is configured correctly. See [Set up Project Griffon](../set-up-project-griffon).

Verify the session matches the link and is input correctly for the expected session. See [Log message "OrgID information is not available"](#sdk-log-message-orgid-information-is-not-available).



## SDK log message "OrgID information is not available"

Verify the AppID is correct in the Mobile Core `configureWithAppID` method.

Make sure you have published the configuration with [Experience Platform Launch](https://launch.adobe.com/). See [Publish the configuration](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property#publish-the-configuration).

Example log messages:

```
(Android) E/AdobeExperienceSDK: Griffon - Org id is null or empty
(Android) D/AdobeExperienceSDK: Griffon - Unable to start griffon session experience cloud OrgID is not available. Verify if the MobileCore is aptly configured.

(iOS) ERROR <ACPGriffon>]: Unable to start griffon session experience cloud OrgID is not available. Verify if the ACPCore is aptly configured.
```



## SDK log message "Timeout"

This log message is not a problem by itself. It is expected if the app was not launched with a Griffon deep link.

Example log messages:
```
(Android) D/AdobeExperienceSDK: Griffon - Timeout - Griffon did not receive deeplink to start griffon session within 5 seconds. Shutting down griffon extension

(iOS) [AdobeExperienceSDK DEBUG <ACPGriffon>]: Timeout - Griffon didnot receive deeplink to start griffon session. Shutting down griffon extension
```



## SDK log message "Failed to show fullscreen takeover"

This log message is not a problem and will appear with typical usage.

Example log message:
```
(Android) E/AdobeExperienceSDK: Griffon - Failed to show fullscreen takeover, could not get fullScreenTakeover object.
```