# Mini Program SDK FAQ

## Frequently asked questions

### After following the listed steps to implement the SDK for WeChat Mini Programs, I still don't see data in my Adobe Analytics report suite - what can I do?
Here's a checklist of solutions you may consider:

* Use the debug tool within the WeChat IDE Devtools or a network proxy monitor (for example Charles) to ensure that your MiniP rogram is sending network requests to Adobe with correct settings - for example network hits contain appropriate Adobe Analytics tracking server and report suite(s) values; context variables or `s` parameters.
* Ensure appropriate timestamp configuration in the SDK is aligned with report suite time stamp settings. That is, `analytics.offlineEnabled` in the SDK configuration block for the Mini Program is aligned with the setting of Timestamp Configuration in your report suite. You may find Timestamp at  Analytics > Admin > Report Suites > General > Timestamp Configuration.
E.g. 
 * `analytics.offlineEnabled = true` ties to Timestamps required or optional
 * `analytics.offlineEnabled = false` ties to Timestamps not allowed or optional       
* Contact Adobe Customer Care

### Tencent requires ICP on all the domains requested by WeChat Mini Programs. Does *sc.adobedc.cn have an ICP provided for by Adobe?
Yes Adobe has an ICP for *.adobedc.cn. You don’t need to apply for an ICP for subdomain of *.adobedc.cn.

### Can I use [Adobe Experience Platform Launch](https://launch.adobe.com) to configure & deploy this SDK?
Deployment through Adobe Experience Platform Launch for this SDK is not yet supported.

### Can I use [Mobile Services](https://mobilemarketing.adobe.com) to configure & deploy this SDK?
Deployment through Mobile Services for this SDK is not yet supported. However, you may use configuration related (report suite, tracking server, etc.) associated with an app created in Mobile Services. Additionally, variable mapping associated with an app in Mobile Services will apply on data sent to Adobe Analytics through the SDK.

### How can I set products variables in the SDK for WeChat Mini Programs? 
As is the case with the Adobe Experience Platform Mobile SDK, products variable cannot be set by using processing rules. To set the products variable for WeChat Mini Programs, you may context data key to “&&products”, and set the value by using the syntax that is defined for the products variable:
“&&products”: “Category;Product;Quantity;Price[,Category;Product;Quantity;Price]”
```javascript
AdobeSDK.trackAction('AddToCart',
{
  "&&events":"scAdd",
  "&&products": ";running shoes;1;69.95,;running socks;10;29.99"
});
```

### When sending data from mini-program to Adobe Analytics, should I use context variable and processing rule? Can I send eVars and events directly to Adobe Analytics? 
Although it is supported to send eVars, events directly to Analytics with WeChat SDK, we recommend sending data in context variable and using processing rules to manage them.


### Does Adobe WeChat SDK support tracking the hybrid mini-program? (hybrid means embedding html page in the native WeChat mini-program)
Yes. As long as the Adobe tracking server is configured in Server Domain Name, you should be able to track hybrid WMP with Adobe WeChat SDK.


### Can this SDK be used for "hybrid" visitor identification use cases?
Hybrid use cases such as tracking users who move from the Mini Program to a web page or if web pages are embedded within a Mini Program are not possible at this time.
These use cases require the Experience Cloud Identity Service, which is not yet available for this SDK.
