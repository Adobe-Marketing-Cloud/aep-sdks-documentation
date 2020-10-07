# Assurance SDK Error Logs

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
(Android) E/AdobeExperienceSDK: Griffon - Failed to show fullscreen takeover, could not get fu
```

