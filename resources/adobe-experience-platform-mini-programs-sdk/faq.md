# Frequently Asked Questions

### I don't see data in my Adobe Analytics report suite - what can I do?

If you have followed our documentation and are unable to see reporting data in your Adobe Analytics dashboard, please consider the following next steps:

#### Verify that network requests are sent to Adobe Analytics

You may use the debug tools in [WeChat DevTools](https://developers.weixin.qq.com/miniprogram/en/dev/devtools/devtools.html) or in a network proxy monitor \(such as [Charles](https://www.charlesproxy.com/) or [Fiddler](https://www.telerik.com/fiddler)\) to ensure that your Mini Program is sending network requests to Adobe Analytics.

For example, network hits to Adobe Analytics will contain values from your SDK configuration block such as tracking server and report suite\(s\) values; context variables or `s` parameters.

#### Ensure appropriate time-stamp configuration

Ensure that your SDK timestamp configuration is aligned with the report suite's time stamp settings. That is, `analytics.offlineEnabled` in the SDK configuration block for the Mini Program is aligned with the setting of Timestamp Configuration in your report suite. You may find Timestamp at  Analytics &gt; Admin &gt; Report Suites &gt; General &gt; Timestamp Configuration.

The following settings explain how settings between the SDK and your report suite should be aligned:

* `analytics.offlineEnabled = true` ties to Timestamps required or optional
* `analytics.offlineEnabled = false` ties to Timestamps not allowed or optional       

#### Contact Adobe Customer Care

If you are unable to resolve your concerns through resources provided here, please contact [Adobe Experience Cloud customer care](https://helpx.adobe.com/contact/enterprise-support.ec.html) for immediate assistance.

### Do Adobe Analytics-provided tracking servers have an ICP?

As Tencent requires ICP on all the domains requested by WeChat Mini Programs, Adobe Analytics tracking servers have a wildcard ICP \(`*.adobedc.cn`\). That is, your tracking server \(typically of the format `yourcompany.adobedc.cn`_\)_ has an ICP. You do not need to separately apply for an ICP for subdomain of `yourcompany.adobedc.cn`.

### Can I use [Adobe Experience Platform Launch](https://launch.adobe.com) to configure & deploy this SDK?

Deployment through Adobe Experience Platform Launch for this SDK is not yet supported.

### Can I use [Mobile Services](https://mobilemarketing.adobe.com) to configure & deploy this SDK?

Deployment through Mobile Services for this SDK is not yet supported. However, you may use configuration related \(report suite, tracking server, etc.\) associated with an app created in Mobile Services. Additionally, variable mapping associated with an app in Mobile Services will apply on data sent to Adobe Analytics through the SDK.

### Can I set products variables?

As is the case with the Adobe Experience Platform Mobile SDK, products variable may not be set by using processing rules.

Instead,  you may use context data key “&&products”, and set values by using the syntax that is defined for the products variable: “&&products”:“Category;Product;Quantity;Price\[,Category;Product;Quantity;Price\]”

```javascript
AdobeSDK.trackAction('AddToCart',
{
  "&&events":"scAdd",
  "&&products": ";running shoes;1;69.95,;running socks;10;29.99"
});
```

### Can I send props & eVars to Adobe Analytics instead of context data?

While it is possible to send props, eVars, events, etc. to Adobe Analytics with the SDK, we strongly recommend collecting & sending context data variables instead. You may then use processing rules simplify data collection and manage content as sent in for reporting.

For more information, please see [Processing Rules Overview](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html).

### Does the SDK support tracking the "hybrid" Mini Programs?

Hybrid use cases such as embedding html pages in native WeChat mini-programs are supported. Ensure that the Adobe Analytics tracking server is appropriately configured in the Server Domain Name value to correctly track hybrid Mini Programs.

### Can the SDK be used for "hybrid" visitor identification use cases?

Hybrid use cases such as tracking users who move from the Mini Program to a web page or if web pages are embedded within a Mini Program are not possible at this time. These use cases require the Experience Cloud Identity Service, which is not yet available for this SDK.

