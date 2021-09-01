# Upgrade to the Experience Platform SDKs

This section contains a checklist that you can use as you plan your upgrade to the Experience Platform SDKs.

{% hint style="danger" %}
The Experience Platform SDK contains **breaking changes** from the 4x SDKs.

In addition to changed APIs, the new SDK includes new APIs and deprecation of APIs such as timed action and milestone media video tracking.
{% endhint %}

### Important considerations

The Experience Platform SDK have been significantly architecturally re-designed, which changes how customers implement and leverage the SDKs.

Review the following checklist to understand some of the changes and what is required to upgrade:

* The Experience Platform SDKs introduce the [Mobile Core](../../foundation-extensions/mobile-core/) and constituent extensions.

  Mobile Core contains core SDK functionality that is required for all implementations that require Adobe and/or third-party extensions.

* The Mobile Core and other extensions are configured in Launch in a mobile property.

  When published, Launch hosts this property configuration and makes it for your SDK implementation.

* You decide which SDK extensions to add, configure, and ultimately include in your app project.

  This provides the flexibility to customize your implementations.

  **Important**: Some extensions depend on others for proper functioning, and these are documented where applicable.

* We recommend that you ease your build process by use supported dependency managers, such as Gradle for Android and Cocoapods for iOS. Launch provides inline instructions and specs to help you with this process.

## Upgrade checklist

1. Begin with [Getting Started](../../getting-started/create-a-mobile-property.md) section and ensure that you are appropriately provisioned for Launch.
2. Ensure all of the required SDK APIs that you currently use are available in the new SDK.

   For more information, see [Experience Platform SDKs vs. the 4x SDK](aepvs4x.md)s.

   **Tip**: The Experience Platform SDK supports iOS versions 10+, Android 4+ \(API 14+\).

3. If you are implementing Analytics, see [Processing rules overview](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=en) to map the variables and rules.
4. In the Experience Platform SDK, you need to manually implement your Lifecycle calls. For more information, see [Manual Lifecycle Implementation](manual-lifecycle-implementation.md).

{% hint style="success" %}
The Experience Platform SDK automatically performs migration tasks that are required to preserve locally stored user context. Without manual intervention, you should expect no change to your visitor reporting or marketing campaigns.
{% endhint %}

{% hint style="info" %}
This client-side, SDK upgrade does not affect marketing campaigns that are in progress, reporting, or other app activities that are configured in Experience Cloud solutions.
{% endhint %}

## Additional information

* See [Experience Cloud vs. 4x SDK functionality comparison](aepvs4x.md)

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://experienceleague.adobe.com/?support-solution=General#support) for immediate assistance

