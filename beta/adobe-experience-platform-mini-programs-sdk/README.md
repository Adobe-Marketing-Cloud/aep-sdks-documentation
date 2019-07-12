# WeChat Mini Programs

The Adobe Experience Platform SDK for WeChat Mini Programs brings Adobe Experience Cloud & Adobe Experience Platform functionality to developers building Mini Programs. The scope for the beta and subsequent general release will be functionality for Adobe Analytics customers who want to track behavioral usage of branded Mini Programs.

{% hint style="warning" %}
This functionality is currently in beta. Contact your Adobe account representatives or CSM to learn more and participate in this beta.
{% endhint %}

## Supported functionality

The SDK for WeChat Mini Programs will provide the following functionality:

### **Configuration** 

The SDK will allow for easy configuration of app and Adobe Analytics related settings. Developers will be able to manage queuing of Analytics requests. Queuing requests canensure HTTP request ordering and potentially minimize quota collision enforced by WeChat. Debug logging \(with multiple log levels\) is also provided for a more transparent implementation.

### **Data Collection** 

The SDK will automatically collect out-of-the-box lifecycle metrics and send to Adobe Analytics for reporting. Developers may also implement custom action, event, and screen tracking.

### Identity 

The SDK will automatically generate an Adobe Analytics Visitor ID \(aid\) to identify program users. Experience Cloud ID \(ECID or MCID\) is not supported at this time.

{% hint style="info" %}
To learn more about Analytics Visitor ID, see the [Adobe Analytics implementation guide](https://docs.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-analytics.html#concept_74F6B4B9B2FA415AB5D029A1F8F099BC).
{% endhint %}

### **Licensing**

The SDK will be available as read-only open source, distributed with an Apache 2.0 license.

