# Upgrading to the Adobe Experience Platform SDKs

This page contains a checklist that you may consider as you decide to upgrade to the Experience Platform SDKs. 

{% hint style="danger" %}
**The Experience Platform SDK contains breaking changes from the 4x SDK**. In addition to changed APIs, the new SDK includes new APIs as well as deprecation of APIs such as timed action and milestone media video tracking.
{% endhint %}

### Important considerations

The Experience Platform SDK has experienced significant architectural re-design and comes with a major paradigm shift in terms of how customers may implement and leverage SDK functionality. The following checklist should help you understand some of these changes and what's required to move forward:

1. The new Experience Platform SDKs introduce the notion of a [Mobile Core](../../using-mobile-extensions/mobile-core/) and constituent extensions. The Mobile Core contains core SDK functionality required for all implementations that require Adobe and/or third-party extensions.
2. Mobile Core and extensions are configured in Launch within a mobile property. When published, Launch hosts this property configuration and makes it for your SDK implementation.
3. You get to decide what SDK extensions to add, configure, and ultimately include in your app project - giving you the flexibility to customize your implementations. Note, however, certain extensions depend on others for proper functioning - these are documented where applicable.
4. We recommend easing your build process by leveraging dependency managers we support such as Gradle for Android and Cocoapods for iOS. Launch provides inline instructions and specs to help you with this process. 

## Upgrade checklist

1. Begin with [Getting Started](../../getting-started/create-a-mobile-property.md) section, ensure you are appropriately provisioned for Launch
2. Ensure all required SDK APIs you currently use are available in the new SDK \(see [AEP vs. 4x SDK](aepvs4x.md) \)
3. Note that Experience Platform SDK supports iOS versions 10+, Android 4+ \(API 14+\)
4. If implementing Analytics, use [Analytics processing rules](https://marketing.adobe.com/resources/help/en_US/reference/processing_rules.html) to map variables/rules

{% hint style="success" %}
The Experience Platform SDK automatically performs migration tasks as required to preserves locally stored user context. Without any manual intervention, you should expect no change to your visitor reporting or marketing campaigns.
{% endhint %}

{% hint style="info" %}
This client-side, SDK upgrade does not affect in-progess marketing campaigns, reporting, or other app activities configured in Adobe Experience Cloud solutions.
{% endhint %}

## Further reading

* See [Experience Cloud vs. 4x SDK functionality comparison](aepvs4x.md) 
* Visit and ask questions on our [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to get quick, thorough responses

