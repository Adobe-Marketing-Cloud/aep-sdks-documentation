# WeChat Mini Programs

The Adobe Experience Platform SDK for WeChat Mini Programs brings Adobe Experience Cloud & Adobe Experience Platform functionality to developers building Mini Programs. The scope for this general release contains functionality for Adobe Analytics customers who want to track behavioral usage of branded Mini Programs.

## Supported functionality

The SDK for WeChat Mini Programs provides the following functionality:

{% tabs %}
{% tab title="English" %}
### **Configuration**

The SDK allows for easy configuration of app and Adobe Analytics related settings. Developers will be able to manage queuing of Analytics requests. Queuing requests can ensure HTTP request ordering and potentially minimize quota collision enforced by WeChat. Debug logging \(with multiple log levels\) is also provided for a more transparent implementation.

### **Data Collection**

The SDK automatically collects out-of-the-box lifecycle metrics and sends it to Adobe Analytics for reporting. Developers may also implement custom action, event, and screen tracking.

### Identity

The SDK generates an Adobe Analytics Visitor ID \(aid\) to identify program users. **Experience Cloud ID \(ECID or MCID\) is not supported at this time**.

{% hint style="info" %}
To learn more about Analytics Visitor ID, see the [Adobe Analytics implementation guide](https://docs.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-analytics.html#concept_74F6B4B9B2FA415AB5D029A1F8F099BC).
{% endhint %}

### **Licensing**

The SDK is available as read-only open source, distributed with an Apache 2.0 license.
{% endtab %}

{% tab title="中文 – 简体" %}
### 配置

* Adobe Analytics 以及小程序基本信息相关配置
* Http 请求队列，避免小程序Http并发请求限制
* 调试日志

### 数据统计

* 小程序生命周期数据的收集，包括安装、启动等事件，以及使用时长等信息
* 自定义的页面、事件信息的收集

### 用户识别

* 使用Analytics Visitor ID标识用户
* 从服务器端获取或者小程序端自动生成

{% hint style="info" %}
有关Analytics Visitor ID的信息，请参阅 [Adobe Analytics implementation guide](https://docs.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-analytics.html#concept_74F6B4B9B2FA415AB5D029A1F8F099BC)
{% endhint %}

### 文档与授权

* 提供英文的帮助文档
* SDK代码采用Apache 2.0开源协议
{% endtab %}
{% endtabs %}

