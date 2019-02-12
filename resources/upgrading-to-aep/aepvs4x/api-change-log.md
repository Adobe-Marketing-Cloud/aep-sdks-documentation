# API Change Log

This page details SDK API changes between the Experience Platform SDK and 4x SDKs.

## Mobile Core APIs <a id="audience-manager-extension-apis"></a>

For more information, see [Mobile Core API reference](../../../using-mobile-extensions/mobile-core/configuration-reference/mobile-core-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| extensionVersion | version/getVersion \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [getPrivacyStatus](../../privacy-and-gdpr.md#set-and-get-privacy-status) | privacyStatus \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [setPrivacyStatus](../../privacy-and-gdpr.md#set-and-get-privacy-status) | setPrivacyStatus: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [setLogLevel](../../../getting-started/initialize-the-sdk.md#enable-debug-logging) | setDebugLogging: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [lifecycleStart:](../../../using-mobile-extensions/mobile-core/lifecycle/lifecycle-api-reference.md#lifecycle-start-and-pause) | collectLifecycleData \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [lifecycleStart:](../../../using-mobile-extensions/mobile-core/lifecycle/lifecycle-api-reference.md#collect-additional-data-with-lifecycle) | collectLifecycleWithAdditionalData \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [lifecycleStop:](../../../using-mobile-extensions/mobile-core/lifecycle/lifecycle-api-reference.md#lifecycle-start-and-pause) | Not applicable |
| [configureWithFileInPath:](../../../using-mobile-extensions/mobile-core/configuration-reference/#using-a-bundled-file-configuration) | overrideConfigPath: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [configureWithAppId:](../../../using-mobile-extensions/mobile-core/configuration-reference/#launch-environment-id) | Not applicable |
| [updateConfiguration:](../../../using-mobile-extensions/mobile-core/configuration-reference/#programmatic-updates-to-configuration) | Not applicable |
| setAppGroup: | setAppGroup: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/ios_ext.html)\) |
| [trackState:data:](../../../using-mobile-extensions/mobile-core/configuration-reference/mobile-core-api-reference.md#track-app-states-and-views) | trackState:data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/states.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/states.html)\) |
| [trackAction:data:](../../../using-mobile-extensions/mobile-core/configuration-reference/mobile-core-api-reference.md#track-app-states-and-views) | trackAction:data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html)\) |
| [collectPII:](../../../using-mobile-extensions/mobile-core/configuration-reference/mobile-core-api-reference.md#collect-pii) | collectPII: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/c_pii-postbacks.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_pii-postbacks.html)\) |
| [getSdkIdentities:](../../../using-mobile-extensions/mobile-core/identity/identity-api-reference.md#get-identifiers) | getAllIdentifiersAsync: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/c_mob_gdpr_ret-stored-ids-ios.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_mob_gdpr_ret-stored-ids-android.html)\) |

### Deprecated APIs & Functionality

| 4x SDK | Notes |
| :--- | :--- |
| trackActionFromBackground \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html)\) | Deprecated |
| trackLocation:data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/geo_poi.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/geo_poi.html)\) | Deprecated |
| trackBeacon:Data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/ibeacon.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/beacon.html)\) | Deprecated |
| trackingClearCurrentBeacon \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/ibeacon.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/beacon.html)\) | Deprecated |
| registerAdobeDataCallback: \([Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) | Deprecated |
| keepLifecycleSessionAlive | Deprecated |
| lifetimeValue \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/lifetime_value.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/lifetime_value.html)\) | Deprecated |
| trackLifetimeValueIncrease:data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/lifetime_value.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/lifetime_value.html)\) |  |
| trackTimedActionStart: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | Deprecated |
| trackTimedActionUpdate: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | Deprecated |
| trackTimedActionEnd: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | Deprecated |
| trackTimedActionExists: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | Deprecated |
| Tracking App Crash \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/crashes.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/crashes.html)\) | Deprecated |

## Adobe Analytics Extension APIs <a id="audience-manager-extension-apis"></a>

For more information, see [Analytics API reference](../../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| [getUserIdentifier:](../../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#getcustomidentifier) | getUserIdentifier \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [setUserIdentifier:](../../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#setcustomidentifier) | setUserIdentifier \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [getTrackingIdentifier:](../../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#gettrackingidentifier) | trackingIdentifier \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/sdk_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/methods.html)\) |
| [sendQueuedHits:](../../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#sendqueuedhits) | trackingSendQueuedHits \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html)\) |
| clearQueue | trackingClearQueue \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html)\) |
| [getQueueSize](../../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#sendqueuedhits-1) | trackingGetQueueSize \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/ios/analytics_methods.html)\) |

## Adobe Audience Manager Extension APIs <a id="audience-manager-extension-apis"></a>

For more information, see [Audience Manager Extension API Reference](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md).

### Supported APIs <a id="supported-apis"></a>

| Experience Platform SDK | 4x SDK \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) |
| :--- | :--- |
| extensionVersion | Not applicable |
| [​getVisitorProfile​](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#get-visitor-profile) | audienceVisitorProfile |
| [​signalWithData:callback:​](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#send-signals-to-audience-manager) | audienceSignalWithData:callback |
| [​reset​](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#reset-identifiers-and-profiles) | audienceReset |

### Deprecated APIs <a id="deprecated-apis"></a>

| 4x SDK | Notes |
| :--- | :--- |
| audienceSetDpid:dpuuid: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |
| audienceDpid: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |
| audienceDpuuid: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |

