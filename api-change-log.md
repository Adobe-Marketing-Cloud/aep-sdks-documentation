# Version 4 API Changelog

This page details SDK API changes between the Experience Platform SDKs and 4x SDKs.

## Mobile Core APIs <a id="audience-manager-extension-apis"></a>

For more information, see [Mobile Core API reference](foundation-extensions/mobile-core/mobile-core-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| extensionVersion | version/getVersion \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [getPrivacyStatus](resources/privacy-and-gdpr.md#set-and-get-privacy-status) | privacyStatus \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [setPrivacyStatus](resources/privacy-and-gdpr.md#set-and-get-privacy-status) | setPrivacyStatus: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [setLogLevel](getting-started/initialize-the-sdk.md#enable-debug-logging) | setDebugLogging: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [configureWithFileInPath:](api-change-log.md) | overrideConfigPath: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [configureWithAppId:](api-change-log.md) | Not applicable |
| [updateConfiguration:](api-change-log.md) | Not applicable |
| setAppGroup: | setAppGroup: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/ios-ext/ios-ext.html?lang=en)\) |
| [trackState:data:](foundation-extensions/mobile-core/mobile-core-api-reference.md#track-app-states-and-views) | trackState:data: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/states.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/states.html?lang=en)\) |
| [trackAction:data:](foundation-extensions/mobile-core/mobile-core-api-reference.md#track-app-states-and-views) | trackAction:data: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/actions.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/actions.html?lang=en)\) |
| [collectPII:](foundation-extensions/mobile-core/mobile-core-api-reference.md#collect-pii) | collectPII: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/postbacks/c-pii-postbacks.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/postbacks/c-pii-postbacks.html?lang=en)\) |
| [getSdkIdentities:](foundation-extensions/mobile-core/identity/identity-api-reference.md#getidentifiers) | getAllIdentifiersAsync: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/privacy-gdpr-ios/c-mob-gdpr-ret-stored-ids-ios.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/c-mob-gdpr-ret-stored-ids-android.html?lang=en)\) |

### Deprecated APIs and functionality

| 4x SDK | Notes |
| :--- | :--- |
| trackActionFromBackground \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/actions.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/actions.html?lang=en)\) | Deprecated |
| trackLocation:data: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/location-ios/geo-poi.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/location/geo-poi.html?lang=en)\) | Deprecated |
| trackBeacon:Data: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/location-ios/ibeacon.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/location/beacon.html?lang=en)\) | Support modified, [see guide](resources/user-guides/track-beacon.md) |
| trackingClearCurrentBeacon \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/location-ios/ibeacon.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/location/beacon.html?lang=en)\) | Deprecated |
| registerAdobeDataCallback: \([Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) | Deprecated |
| lifetimeValue \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/lifetime-value.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/lifetime-value.html?lang=en)\) | Deprecated |
| trackLifetimeValueIncrease:data: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/lifetime-value.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/lifetime-value.html?lang=en)\) |  |
| trackTimedActionStart: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/timed-actions.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/timed-actions.html?lang=en)\) | Deprecated |
| trackTimedActionUpdate: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/timed-actions.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/timed-actions.html?lang=en)\) | Deprecated |
| trackTimedActionEnd: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/timed-actions.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/timed-actions.html?lang=en)\) | Deprecated |
| trackTimedActionExists: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/timed-actions.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/timed-actions.html?lang=en)\) | Deprecated |
| trackPushMessageClickThrough:userInfo\([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/messaging-ios/push-messaging/push-messaging.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/messaging-android/push-messaging/push-messaging.html?lang=en)\) | Support modified, [see guide](https://aep-sdks.gitbook.io/docs/resources/frequently-asked-questions#how-can-i-track-user-engagement-of-push-notifications-using-the-experience-platform-mobile-sdk) |
| Tracking App Crash \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/crashes.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/crashes.html?lang=en)\) | Deprecated |

## Lifecycle extension APIs

### Supported APIs

{% hint style="warning" %}
In the v4 iOS SDK, Lifecycle `start` and `stop` calls are made automatically by the SDK. In the AEP SDK, the calls to start and stop lifecycle will need to be made by the application developer. For more information, see [Lifecycle extension in iOS](foundation-extensions/mobile-core/lifecycle/lifecycle-extension-in-ios.md).
{% endhint %}

For more information, see [Lifecycle API reference](foundation-extensions/mobile-core/lifecycle/lifecycle-api-reference.md).

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| [lifecycleStart:](foundation-extensions/mobile-core/lifecycle/lifecycle-api-reference.md#lifecycle-start-and-pause) | collectLifecycleData \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [lifecycleStart:](foundation-extensions/mobile-core/lifecycle/lifecycle-api-reference.md#collect-additional-data-with-lifecycle) | collectLifecycleWithAdditionalData \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [lifecycleStop](foundation-extensions/mobile-core/lifecycle/lifecycle-api-reference.md#lifecycle-start-and-pause) | pauseCollectingLifecycleData \([Android only](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |

### Deprecated APIs

| 4x SDK | Notes |
| :--- | :--- |
| keepLifecycleSessionAlive \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) | Deprecated |

## Identity extension APIs

For more information, see [Identity API reference](foundation-extensions/mobile-core/identity/identity-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| [setPushIdentifier:](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#setpushidentifier) | setPushIdentifier \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [setAdvertisingIdentifier:](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#setadvertisingidentifier) | setAdvertisingIdentifier \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [getExperienceCloudId:](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#getexperiencecloudid) | visitorMarketingCloudID \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/exp-cloud-ios/mc-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/experience-cloud-android/mc-methods.html?lang=en)\) |
| [syncIdentifiers:](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#syncidentifiers) | visitorSyncIdentifiers \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/exp-cloud-ios/mc-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/experience-cloud-android/mc-methods.html?lang=en)\) |
| [syncIdentifiers:authentication:](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#syncidentifiers-overloaded) | visitorSyncIdentifiers:authenticationState: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/exp-cloud-ios/mc-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/experience-cloud-android/mc-methods.html?lang=en)\) |
| [syncIdentifier:identifier:authentication:](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#syncidentifier) | visitorSyncIdentifiersWithType:identifier:authenticationState: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/exp-cloud-ios/mc-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/experience-cloud-android/mc-methods.html?lang=en)\) |
| [getIdentifiers](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#getidentifiers) | visitorGetIDs \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/exp-cloud-ios/mc-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/experience-cloud-android/mc-methods.html?lang=en)\) |
| [appendToURL:withCallback:](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#appendtourl-appendvisitorinfoforurl) | visitorAppendToURL: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/exp-cloud-ios/mc-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/experience-cloud-android/mc-methods.html?lang=en)\) |
| [getUrlVariables](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#geturlvariables) | visitorGetUrlVariablesAsync: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/sdk-reference-ios/hybrid-app.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/sdk-reference-android/hybrid-app.html?lang=en)\) |

## Adobe Analytics extension APIs <a id="audience-manager-extension-apis"></a>

For more information, see [Analytics API reference](using-mobile-extensions/adobe-analytics/analytics-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| [getUserIdentifier:](using-mobile-extensions/adobe-analytics/analytics-api-reference.md#getcustomidentifier) | getUserIdentifier \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [setUserIdentifier:](using-mobile-extensions/adobe-analytics/analytics-api-reference.md#setcustomidentifier) | setUserIdentifier \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [getTrackingIdentifier:](using-mobile-extensions/adobe-analytics/analytics-api-reference.md#gettrackingidentifier) | trackingIdentifier \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/sdk-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/configuration-android/methods.html?lang=en)\) |
| [sendQueuedHits:](using-mobile-extensions/adobe-analytics/analytics-api-reference.md#sendqueuedhits) | trackingSendQueuedHits \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/analytics-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/analytics-methods.html?lang=en)\) |
| clearQueue | trackingClearQueue \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/analytics-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/analytics-methods.html?lang=en)\) |
| [getQueueSize](using-mobile-extensions/adobe-analytics/analytics-api-reference.md#sendqueuedhits-1) | trackingGetQueueSize \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/analytics-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/analytics-methods.html?lang=en)\) |

## Adobe Audience Manager extension APIs <a id="audience-manager-extension-apis"></a>

For more information, see [Audience Manager Extension API Reference](using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md).

### Supported APIs <a id="supported-apis"></a>

| Experience Platform SDK | 4x SDK \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/aam-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/audience-manager-android/c-audience-manager-methods.html?lang=en)\) |
| :--- | :--- |
| extensionVersion | Not applicable |
| [​getVisitorProfile​](using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#get-visitor-profile) | audienceVisitorProfile |
| [​signalWithData:callback:​](using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#send-signals-to-audience-manager) | audienceSignalWithData:callback |
| [​reset​](using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#reset-identifiers-and-profiles) | audienceReset |

### Deprecated APIs <a id="deprecated-apis"></a>

| 4x SDK | Notes |
| :--- | :--- |
| audienceSetDpid:dpuuid: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/aam-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/audience-manager-android/c-audience-manager-methods.html?lang=en)\) | Replaced - See [Link](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/cid.html?lang=en)​ |
| audienceDpid: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/aam-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/audience-manager-android/c-audience-manager-methods.html?lang=en)\) | Replaced - See [Link](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/cid.html?lang=en)​ |
| audienceDpuuid: \([iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/aam-methods.html?lang=en) \| [Android](https://experienceleague.adobe.com/docs/mobile-services/android/audience-manager-android/c-audience-manager-methods.html?lang=en)\) | Replaced - See [Link](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/cid.html?lang=en)​ |

## Adobe Target extension APIs

For more information see [Target API reference](using-mobile-extensions/adobe-target/target-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK \(iOS \| Android\) |
| :--- | :--- |
| getThirdPartyId: | targetThirdPartyID |
| setThirdPartyId: | targetSetThirdPartyID |
| getTntId: | Not applicable |
| resetExperience: | targetClearCookies |
| targetPrefetchObjectWithName:targetParameters: | targetPrefetchObjectWithName:mboxParameters: |
| prefetchContent:withParameters:callback: | targetPrefetchContent:withProfileParameters:callback: |
| prefetchClearCache: | targetPrefetchClearCache |
| targetRequestObjectWithName:targetParameters:defaultContent:callback: | targetRequestObjectWithName:defaultContent:mboxParameters:callback: |
| retrieveLocationContent:withParameters: | targetLoadRequests:withProfileParameters: |
| locationClickedWithName:targetParameters: | locationClickedWithName:mboxParameters:productParameters:orderParameters: |
| setPreviewRestartDeeplink: | targetPreviewRestartDeepLink: |

### Deprecated APIs

| 4x SDK | Notes |
| :--- | :--- |
| targetPcID | Deprecated |
| targetSessionID | Deprecated |
| targetLoadRequest:callback: | Deprecated |
| targetLoadRequestWithName:defaultContent:profileParameters:orderParameters:mboxParameters:callback: | Deprecated |
| targetLoadRequestWithName:defaultContent:profileParameters:orderParameters:mboxParameters:requestLocationParameters:callback: | Deprecated |
| targetCreateRequestWithName:defaultContent:parameters: | Deprecated |
| targetCreateOrderConfirmRequestWithName:orderId:orderTotal:productPurchasedId:parameters: | Deprecated |

