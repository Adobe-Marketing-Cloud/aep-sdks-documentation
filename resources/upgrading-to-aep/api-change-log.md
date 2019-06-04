# API Changelog

This page details SDK API changes between the Experience Platform SDKs and 4x SDKs.

## Mobile Core APIs    <a id="audience-manager-extension-apis"></a>

For more information, see [Mobile Core API reference](../../using-mobile-extensions/mobile-core/mobile-core-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| extensionVersion | version/getVersion \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [getPrivacyStatus](../privacy-and-gdpr.md#set-and-get-privacy-status) | privacyStatus \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [setPrivacyStatus](../privacy-and-gdpr.md#set-and-get-privacy-status) | setPrivacyStatus: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [setLogLevel](../../getting-started/initialize-the-sdk.md#enable-debug-logging) | setDebugLogging: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [configureWithFileInPath:](api-change-log.md) | overrideConfigPath: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [configureWithAppId:](api-change-log.md) | Not applicable |
| [updateConfiguration:](api-change-log.md) | Not applicable |
| setAppGroup: | setAppGroup: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/ios_ext.html)\) |
| [trackState:data:](../../using-mobile-extensions/mobile-core/mobile-core-api-reference.md#track-app-states-and-views) | trackState:data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/states.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/states.html)\) |
| [trackAction:data:](../../using-mobile-extensions/mobile-core/mobile-core-api-reference.md#track-app-states-and-views) | trackAction:data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html)\) |
| [collectPII:](../../using-mobile-extensions/mobile-core/mobile-core-api-reference.md#collect-pii) | collectPII: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/c_pii-postbacks.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_pii-postbacks.html)\) |
| [getSdkIdentities:](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#get-identifiers) | getAllIdentifiersAsync: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/c_mob_gdpr_ret-stored-ids-ios.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_mob_gdpr_ret-stored-ids-android.html)\) |

### Deprecated APIs and functionality

| 4x SDK | Notes |
| :--- | :--- |
| trackActionFromBackground \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html)\) | Deprecated |
| trackLocation:data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/geo_poi.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/geo_poi.html)\) | Deprecated |
| trackBeacon:Data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/ibeacon.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/beacon.html)\) | Deprecated |
| trackingClearCurrentBeacon \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/ibeacon.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/beacon.html)\) | Deprecated |
| registerAdobeDataCallback: \([Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) | Deprecated |
| lifetimeValue \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/lifetime_value.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/lifetime_value.html)\) | Deprecated |
| trackLifetimeValueIncrease:data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/lifetime_value.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/lifetime_value.html)\) |  |
| trackTimedActionStart: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | Deprecated |
| trackTimedActionUpdate: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | Deprecated |
| trackTimedActionEnd: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | Deprecated |
| trackTimedActionExists: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | Deprecated |
| Tracking App Crash \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/crashes.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/crashes.html)\) | Deprecated |

## Lifecycle extension APIs

### Supported APIs

{% hint style="warning" %}
In the v4 iOS SDK, Lifecycle `start` and `stop` calls are made automatically by the SDK. In the AEP SDK, the calls to start and stop lifecycle will need to be made by the application developer. For more information, see [Lifecycle extension in iOS](../../using-mobile-extensions/mobile-core/lifecycle/lifecycle-extension-in-ios.md).
{% endhint %}

For more information, see [Lifecycle API reference](../../using-mobile-extensions/mobile-core/lifecycle/lifecycle-api-reference.md).

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| [lifecycleStart:](../../using-mobile-extensions/mobile-core/lifecycle/lifecycle-api-reference.md#lifecycle-start-and-pause) | collectLifecycleData \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [lifecycleStart:](../../using-mobile-extensions/mobile-core/lifecycle/lifecycle-api-reference.md#collect-additional-data-with-lifecycle) | collectLifecycleWithAdditionalData \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [lifecycleStop](../../using-mobile-extensions/mobile-core/lifecycle/lifecycle-api-reference.md#lifecycle-start-and-pause) | pauseCollectingLifecycleData \([Android only](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |

### Deprecated APIs

| 4x SDK | Notes |
| :--- | :--- |
| keepLifecycleSessionAlive \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) | Deprecated |

## Identity extension APIs

For more information, see [Identity API reference](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| [setPushIdentifier:](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#set-the-push-identifier) | setPushIdentifier \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [setAdvertisingIdentifier:](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#set-an-advertising-identifier) | setAdvertisingIdentifier \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [getMarketingCloudID:](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#get-experience-cloud-ids) | visitorMarketingCloudID \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/mc_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/mc_methods.html)\) |
| [syncIdentifiers:](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#synch-identifiers) | visitorSyncIdentifiers \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/mc_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/mc_methods.html)\) |
| [syncIdentifiers:authentication:](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#synch-identifiers) | visitorSyncIdentifiers:authenticationState: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/mc_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/mc_methods.html)\) |
| [syncIdentifier:identifier:authentication:](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#synch-identifiers) | visitorSyncIdentifiersWithType:identifier:authenticationState: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/mc_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/mc_methods.html)\) |
| [getIdentifiers](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#get-identifiers) | visitorGetIDs \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/mc_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/mc_methods.html)\) |
| [appendToURL:withCallback:](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#append-visitor-data-to-a-url) | visitorAppendToURL: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/mc_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/mc_methods.html)\) |
| [getUrlVariables](../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#getUrlVariablesTitle) | visitorGetUrlVariablesAsync: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/hybrid_app.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/hybrid_app.html)\) |

## Adobe Analytics extension APIs    <a id="audience-manager-extension-apis"></a>

For more information, see [Analytics API reference](../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| [getUserIdentifier:](../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#getcustomidentifier) | getUserIdentifier \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [setUserIdentifier:](../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#setcustomidentifier) | setUserIdentifier \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [getTrackingIdentifier:](../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#gettrackingidentifier) | trackingIdentifier \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [sendQueuedHits:](../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#sendqueuedhits) | trackingSendQueuedHits \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html)\) |
| clearQueue | trackingClearQueue \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html)\) |
| [getQueueSize](../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#sendqueuedhits-1) | trackingGetQueueSize \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html)\) |

## Adobe Audience Manager extension APIs    <a id="audience-manager-extension-apis"></a>

For more information, see [Audience Manager Extension API Reference](../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md).

### Supported APIs    <a id="supported-apis"></a>

| Experience Platform SDK | 4x SDK \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) |
| :--- | :--- |
| extensionVersion | Not applicable |
| [​getVisitorProfile​](../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#get-visitor-profile) | audienceVisitorProfile |
| [​signalWithData:callback:​](../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#send-signals-to-audience-manager) | audienceSignalWithData:callback |
| [​reset​](../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#reset-identifiers-and-profiles) | audienceReset |

### Deprecated APIs    <a id="deprecated-apis"></a>

| 4x SDK | Notes |
| :--- | :--- |
| audienceSetDpid:dpuuid: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |
| audienceDpid: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |
| audienceDpuuid: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |

## Adobe Target extension APIs

For more information see [Target API reference](../../using-mobile-extensions/adobe-target/target-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK \(iOS \| Android\) |
| :--- | :--- |
| getThirdPartyId: | targetThirdPartyID |
| setThirdPartyId: | targetSetThirdPartyID |
| getTntid: | Not applicable |
| resetExperience: | targetClearCookies |
| prefetchObjectWithName:mboxParameters: | targetPrefetchObjectWithName:mboxParameters: |
| prefetchContent:withProfileParameters:callback: | targetPrefetchContent:withProfileParameters:callback: |
| prefetchClearCache: | targetPrefetchClearCache |
| requestObjectWithName:defaultContent:mboxParameters:callback: | targetRequestObjectWithName:defaultContent:mboxParameters:callback: |
| loadRequests:withProfileParameters: | targetLoadRequests:withProfileParameters: |

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

