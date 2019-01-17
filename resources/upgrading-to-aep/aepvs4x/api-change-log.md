# API Change Log

This page details SDK API changes between the Experience Platform SDK and 4x SDKs.

## Audience Manager Extension APIs <a id="audience-manager-extension-apis"></a>

For more information, see [Audience Manager Extension API Reference](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md).

### Supported APIs <a id="supported-apis"></a>

| Experience Platform SDK | 4x SDK \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) |
| :--- | :--- |
| [​getVisitorProfile​](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#get-visitor-profile) | audienceVisitorProfile |
| [​signalWithData:callback:​](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#send-signals-to-audience-manager) | audienceSignalWithData:callback |
| [​reset​](../../../using-mobile-extensions/adobe-audience-manager/audience-manager-api-reference.md#reset-identifiers-and-profiles) | audienceReset |

### Deprecated APIs <a id="deprecated-apis"></a>

| 4x SDK \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/aam_methods.html) \| [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_audience_manager_methods.html)\) | Notes |
| :--- | :--- |
| _audienceSetDpid:dpuuid:_ | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |
| _audienceDpid_ | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |
| _audienceDpuuid_ | Replaced - See [Link](https://marketing.adobe.com/resources/help/en_US/aam/cid.html)​ |

