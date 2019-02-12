# API Change Log

This page details SDK API changes between the Experience Platform SDK and 4x SDKs.

## Mobile Core API <a id="audience-manager-extension-apis"></a>

For more information, see [Mobile Core API reference](../../../using-mobile-extensions/mobile-core/configuration-reference/mobile-core-api-reference.md).

### Supported APIs

| Experience Platform SDK | 4x SDK |
| :--- | :--- |
| extensionVersion | version |
| getPrivacyStatus | privacyStatus |
| setPrivacyStatus | setPrivacyStatus: |
| setLogLevel | setDebugLogging: |
| lifecycleStart: | collectLifecycleData |
| lifecycleStart: | collectLifecycleWithAdditionalData |
| lifecycleStop: | Not applicable |
| configureWithFileInPath: | overrideConfigPath: |
| configureWithAppId: |  |
| updateConfiguration: |  |
| setAppGroup: | setAppGroup: |
| trackState:data: | trackState:data: |
| trackAction:data: | trackAction:data: |
| collectPII: | collectPII: |
| getSdkIdentities: | getAllIdentifiersAsync: |

### Deprecated APIs

| 4x SDK | Notes |
| :--- | :--- |
| trackActionFromBackground | Deprecated |
| trackLocation:data: | Deprecated |
| trackBeacon:Data: \(iOS\) | Deprecated |
| trackingClearCurrentBeacon \(iOS\) | Deprecated |
| registerAdobeDataCallback: | Deprecated |
| keepLifecycleSessionAlive | Deprecated |
| lifetimeValue | Deprecated |

## Audience Manager Extension APIs <a id="audience-manager-extension-apis"></a>

For more information, see [Audience Manager Extension API Reference](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md).

### Supported APIs <a id="supported-apis"></a>

| Experience Platform SDK | 4x SDK \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) |
| :--- | :--- |
| extensionVersion | Not applicable |
| [​getVisitorProfile​](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#get-visitor-profile) | audienceVisitorProfile |
| [​signalWithData:callback:​](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#send-signals-to-audience-manager) | audienceSignalWithData:callback |
| [​reset​](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#reset-identifiers-and-profiles) | audienceReset |

### Deprecated APIs <a id="deprecated-apis"></a>

| 4x SDK \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) | Notes |
| :--- | :--- |
| _audienceSetDpid:dpuuid:_ | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |
| _audienceDpid_ | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |
| _audienceDpuuid_ | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |

