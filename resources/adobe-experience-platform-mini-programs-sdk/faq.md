# Frequently Asked Questions

{% hint style="warning" %}
While the Adobe Experience Platform SDK for WeChat Mini Programs is complimentarily available for all Adobe customers, the SDK for the WeChat Mini Program requires _in-country_ data collection.

Customers must purchase the _China Performance Optimization Add-On_ for Adobe Analytics in order to use the SDK. Please contact your Adobe account team for further detail.
{% endhint %}

## I don't see data in my Adobe Analytics report suite - what can I do?

If you have followed the documentation and are unable to see reporting data in your Adobe Analytics dashboard, please consider the following next steps:

### Verify that network requests are sent to Adobe Analytics

You can use the debug tools in [WeChat DevTools](https://developers.weixin.qq.com/miniprogram/en/dev/devtools/devtools.html) or in a network proxy monitor, such as [Charles](https://www.charlesproxy.com/) or [Fiddler](https://www.telerik.com/fiddler), to ensure that your Mini Program is sending network requests to Adobe Analytics.

For example, network hits to Adobe Analytics will contain values from your SDK configuration block such as tracking server and report suite\(s\) values; context variables; or `s` parameters.

### Ensure appropriate timestamp configuration

Ensure that your SDK timestamp configuration is aligned with the report suite's timestamp settings by making sure that the `analytics.offlineEnabled` value in the SDK configuration block for the Mini Program is aligned with the setting of Timestamp Configuration in your report suite. You can find timestamp settings at Analytics &gt; Admin &gt; Report Suites &gt; General &gt; Timestamp Configuration.

The following settings explain how settings between the SDK and your report suite should be aligned:

* `analytics.offlineEnabled = true` ties to timestamp-required or timestamp-optional report suites
* `analytics.offlineEnabled = false` ties to timestamp-not-allowed or timestamp-optional report suites

### Contact Adobe Customer Care

If you are unable to resolve your concerns through resources provided here, please contact [Adobe Experience Cloud customer care](https://experienceleague.adobe.com/?support-solution=General#support) for immediate assistance.

## Do Adobe Analytics-provided tracking servers have an ICP?

As Tencent requires ICP on all the domains requested by WeChat Mini Programs, Adobe Analytics tracking servers have a wildcard ICP \(`*.adobedc.cn`\), which means that your tracking server \(typically of the format `yourcompany.adobedc.cn`\) has an ICP. You do not need to separately apply for an ICP for subdomain of `yourcompany.adobedc.cn`.

## Can I use [Adobe Experience Platform Launch](https://launch.adobe.com) to configure and deploy this SDK?

Deployment through Adobe Experience Platform Launch for this SDK is not yet supported.

## Can I use [Mobile Services](https://mobilemarketing.adobe.com) to configure and deploy this SDK?

Deployment through Mobile Services for this SDK is not yet supported. However, you may use related configuration settings \(such as a report suite or a tracking server\) with an app created in Mobile Services. Additionally, variable mapping associated with an app in Mobile Services will apply to data sent to Adobe Analytics through the SDK.

## Can I set products variables?

As is the case with the Adobe Experience Platform Mobile SDK, products variable cannot be set by using processing rules.

Instead, you can use context data key `&&products`, and set values by using the syntax that is defined for the products variable: `"&&products":"Category;Product;Quantity;Price\[,Category;Product;Quantity;Price\]"`

```javascript
AdobeSDK.trackAction('AddToCart',
{
  "&&events":"scAdd",
  "&&products": ";running shoes;1;69.95,;running socks;10;29.99"
});
```

## Can I send props and eVars to Adobe Analytics instead of context data?

While it is possible to send props, eVars, and events to Adobe Analytics with the SDK, you should collect and send context data variables instead. You may then use processing rules simplify data collection and to manage content as it is sent to Adobe Analytics.

For more information, please see the [processing rules overview](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html).

## Does the SDK support tracking the "hybrid" Mini Programs?

Hybrid use cases, such as embedding HTML pages in native WeChat mini-programs, are supported. Ensure that the Adobe Analytics tracking server is appropriately configured in the **Server Domain Name** to correctly track the hybrid Mini Programs.

## Can the SDK be used for "hybrid" visitor identification use cases?

Hybrid use cases, such as tracking users who move from the Mini Program to a web page or tracking web pages that are embedded within a Mini Program, are not possible at this time. These use cases require the Experience Cloud Identity Service, which is not yet available for this SDK.

