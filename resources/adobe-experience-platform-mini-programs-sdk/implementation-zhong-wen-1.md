# Implementation - 中文–简体

本文旨在介绍如何在微信小程序中使用Adobe Experience Platform SDK.

## 添加小程序SDK到项目中

小程序SDK可以从如下地址进行下载：[https://github.com/adobe/wechat/tree/master/dist](https://github.com/adobe/wechat/tree/master/dist)

小程序SDK下载到本地之后，可以将该SDK添加到项目路径下。然后在小程序项目的app.js文件中，引用下载到本地的SDK。例如：

```
const AdobeSDK = require('AdobeSDK.js');
```

## 初始化SDK

在app.js文件中的`onLaunch`方法中，调用`AdobeSDK.init()`，并且注意配置上正确的参数值，例如：

{% hint style="warning" %}
 请联系贵公司的Adobe Analytics管理员或者Adobe咨询顾问来确定这些配置参数。
{% endhint %}

```javascript
// App({
//   onLaunch: function () {
//     // 展示本地存储能力
//     var logs = wx.getStorageSync('logs') || []
//     logs.unshift(Date.now())
//     wx.setStorageSync('logs', logs)
     AdobeSDK.init({
       "analytics.server": "example.sc.adobedc.cn",      //必填
       "analytics.rsids": "example.reportsuite",    //必填
       "app.id": "adobe-demo",                        //必填
       "app.version": "0.0.0.1",           //选填, default value = ''
       "analytics.offlineEnabled": true,   //选填, default value = false
       "session.timeout": 30               //选填, default value = 30
     });
// })
```

{% hint style="info" %}
如果在上述配置中将`analytics.offlineEnabled`配置为True，那么向Analytics发出的请求中会包含timestamps\(ts\).

`session.timeout`这个配置的单位是秒，指的是从App初始化完成开始，到一个新的session之间所经过的时间。这个timeout时间在小程序进入后台，之后被重新激活进入前台运行的场景下同样适用。该配置的缺省值是30秒。
{% endhint %}

{% hint style="info" %}
如果需要将数据发送给多个报表包，可以在相应配置中用逗号分割RSID。例如：

`"analytics.rsids": "example.rsid1,example.rsid2"`。这个写法会把数据发送给`example.rsid1`和`example.rsid2`这两个报表包。
{% endhint %}

SDK初始化完成之后，会自动开始收集数据，并向Adobe Analytics发送生命周期指标。请在[生命周期指标](implementation-zhong-wen-1.md#life-cyclecn-2)查看完整的生命周期指标。

## 启用调试日志功能 <a id="life-cyclecn"></a>

### AdobeSDK.setDebugLoggingEnabled\(flag\)

用如下代码可以启用调试日志功能

```javascript
AdobeSDK.setDebugLoggingEnabled(true)
```

### AdobeSDK.setDebugModeEnabled\(flag\)

确实设置下，本SDK会隐藏异常错误信息。在调试模式下，会将异常错误信息打印在控制台中。用如下代码可以打开调试模式：

```javascript
AdobeSDK.setDebugModeEnabled(true)
```

## 追踪用户行为 <a id="life-cyclecn"></a>

下面介绍在小程序中用来追踪和监测用户行为的API。

### AdobeSDK.trackAction\(actionName, contextData\)

可以使用这个API来追踪和监测用户行为。每一次用户行为会触发事件，进而增加一个或多个相应指标的值。例如，可以用这个API来追踪用户订阅，用户浏览了一篇文章，或者用户升级到新级别。

{% hint style="info" %}
发送给Analytics的`trackAction`请求会被当做一个事件\(**event**\)来处理，这个请求不会增加page view。在发送给Analytics中，会用action这个变量来传送值。
{% endhint %}

```javascript
AdobeSDK.trackAction("action", { "example.key": "value" });
```

### AdobeSDK.trackState\(stateName, contextData\)

{% hint style="info" %}
Analytics会把`trackState`请求当做Page View来处理。`stateName`参数的值会作为Page Name。在发送给Analytics中，会用page name变量来传送值。
{% endhint %}

{% hint style="info" %}
可以在小程序的`onShow`方法中调用该API来追踪用户在不同页面间切换的行为。
{% endhint %}

```javascript
AdobeSDK.trackState("state", { "example.key": "value" });
```

## 生命周期指标 <a id="life-cyclecn"></a>

在SDK初始化完成之后，生命周期指标会被自动发送给Analytics。下表是收集以及发送给Analytics的生命周期指标的完整列表：

### 小程序安装

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x6307;&#x6807;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x6807;&#x8BC6;&#x7B26;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>&#x9996;&#x6B21;&#x6253;&#x5F00;</p>
        <p>(First Launches)</p>
      </td>
      <td style="text-align:left"><code>a.InstallEvent</code>
      </td>
      <td style="text-align:left">&#x9996;&#x6B21;&#x52A0;&#x8F7D;&#x5E76;&#x6253;&#x5F00;&#x5C0F;&#x7A0B;&#x5E8F;&#xFF0C;&#x6216;&#x8005;&#x5C0F;&#x7A0B;&#x5E8F;&#x88AB;&#x5378;&#x8F7D;&#x540E;&#x91CD;&#x65B0;&#x52A0;&#x8F7D;&#x6253;&#x5F00;&#x5C0F;&#x7A0B;&#x5E8F;&#x65F6;&#x89E6;&#x53D1;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x5B89;&#x88C5;&#x65E5;&#x671F;</p>
        <p>(Install Date)</p>
      </td>
      <td style="text-align:left"><code>a.InstallDate</code>
      </td>
      <td style="text-align:left">&#x9996;&#x6B21;&#x6253;&#x5F00;&#x5C0F;&#x7A0B;&#x5E8F;&#x7684;&#x65E5;&#x671F;</td>
    </tr>
  </tbody>
</table>

### 小程序升级

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x6307;&#x6807;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x6807;&#x8BC6;&#x7B26;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>&#x5347;&#x7EA7;</p>
        <p>(Upgrades)</p>
      </td>
      <td style="text-align:left"><code>a.UpgradeEvent</code>
      </td>
      <td style="text-align:left">&#x5C0F;&#x7A0B;&#x5E8F;&#x7248;&#x672C;&#x53F7;&#x6539;&#x53D8;&#x540E;&#xFF0C;&#x7528;&#x6237;&#x9996;&#x6B21;&#x8FD0;&#x884C;&#x5C0F;&#x7A0B;&#x5E8F;&#x65F6;&#x89E6;&#x53D1;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x8DDD;&#x4E0A;&#x6B21;&#x5347;&#x7EA7;&#x5929;&#x6570;</p>
        <p>(Days since last upgrade)</p>
      </td>
      <td style="text-align:left"><code>a.DaysSinceLastUpgrade</code>
      </td>
      <td style="text-align:left">&#x8DDD;&#x4E0A;&#x6B21;&#x5C0F;&#x7A0B;&#x5E8F;&#x7248;&#x672C;&#x53F7;&#x53D8;&#x66F4;&#x540E;&#x7ECF;&#x8FC7;&#x7684;&#x5929;&#x6570;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x81EA;&#x4E0A;&#x6B21;&#x5347;&#x7EA7;&#x540E;&#x6253;&#x5F00;&#x6B21;&#x6570;</p>
        <p>(Launches since last upgrade)</p>
      </td>
      <td style="text-align:left"><code>a.LaunchesSinceUpgrade</code>
      </td>
      <td style="text-align:left">&#x81EA;&#x4E0A;&#x6B21;&#x5C0F;&#x7A0B;&#x5E8F;&#x7248;&#x672C;&#x53D8;&#x66F4;&#x540E;&#xFF0C;&#x6253;&#x5F00;&#x6B21;&#x6570;&#x3002;(&#x6CE8;&#xFF1A;&#x5C0F;&#x7A0B;&#x5E8F;App&#x7684;<code>onLaunch</code>&#x51FD;&#x6570;&#x8C03;&#x7528;&#x6B21;&#x6570;&#xFF09;</td>
    </tr>
  </tbody>
</table>

### 小程序打开

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x6307;&#x6807;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x6807;&#x8BC6;&#x7B26;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>&#x65E5;&#x7528;&#x6237;&#x6570;</p>
        <p>(Daily Engaged Users)</p>
      </td>
      <td style="text-align:left"><code>a.DailyEngUserEvent</code>
      </td>
      <td style="text-align:left">&#x5F53;&#x7528;&#x6237;&#x5728;&#x5F53;&#x65E5;&#x6709;&#x4F7F;&#x7528;&#x5C0F;&#x7A0B;&#x5E8F;&#x65F6;&#x89E6;&#x53D1;&#x3002;<b>&#x91CD;&#x8981;</b>&#xFF1A;Analytics&#x4E0D;&#x4F1A;&#x81EA;&#x52A8;&#x5B58;&#x50A8;&#x8BE5;&#x6307;&#x6807;&#x3002;&#x5982;&#x679C;&#x9700;&#x8981;&#x4F7F;&#x7528;&#x8BE5;&#x6307;&#x6807;&#xFF0C;&#x5FC5;&#x987B;&#x7528;&#x5904;&#x7406;&#x89C4;&#x5219;&#x6765;&#x914D;&#x7F6E;&#x81EA;&#x5B9A;&#x4E49;&#x4E8B;&#x4EF6;&#xFF0C;&#x624D;&#x80FD;&#x8BB0;&#x5F55;&#x8BE5;&#x6307;&#x6807;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6708;&#x7528;&#x6237;&#x6570;(Monthly Engaged Users)</td>
      <td style="text-align:left"><code>a.MonthlyEngUserEvent</code>
      </td>
      <td style="text-align:left">&#x5F53;&#x7528;&#x6237;&#x5728;&#x5F53;&#x6708;&#x6709;&#x4F7F;&#x7528;&#x5C0F;&#x7A0B;&#x5E8F;&#x65F6;&#x89E6;&#x53D1;&#x3002;<b>&#x91CD;&#x8981;</b>&#xFF1A;Analytics&#x4E0D;&#x4F1A;&#x81EA;&#x52A8;&#x5B58;&#x50A8;&#x8BE5;&#x6307;&#x6807;&#x3002;&#x5982;&#x679C;&#x9700;&#x8981;&#x4F7F;&#x7528;&#x8BE5;&#x6307;&#x6807;&#xFF0C;&#x5FC5;&#x987B;&#x7528;&#x5904;&#x7406;&#x89C4;&#x5219;&#x6765;&#x914D;&#x7F6E;&#x81EA;&#x5B9A;&#x4E49;&#x4E8B;&#x4EF6;&#xFF0C;&#x624D;&#x80FD;&#x8BB0;&#x5F55;&#x8BE5;&#x6307;&#x6807;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6253;&#x5F00;&#x6B21;&#x6570;(Launches)</td>
      <td style="text-align:left"><code>a.LaunchEvent</code>
      </td>
      <td style="text-align:left">&#x6BCF;&#x6B21;&#x6253;&#x5F00;&#x5C0F;&#x7A0B;&#x5E8F;&#x8FD0;&#x884C;&#x65F6;&#x89E6;&#x53D1;&#xFF0C;&#x5305;&#x62EC;&#x5C0F;&#x7A0B;&#x5E8F;&#x5D29;&#x6E83;&#x540E;&#x91CD;&#x542F;&#x53CA;&#x5C0F;&#x7A0B;&#x5E8F;&#x9996;&#x6B21;&#x6253;&#x5F00;&#x8FD0;&#x884C;&#x3002;&#x53E6;&#x5916;&#xFF0C;&#x5728;&#x5C0F;&#x7A0B;&#x5E8F;&#x88AB;&#x4ECE;&#x540E;&#x53F0;&#x5524;&#x9192;&#x5230;&#x524D;&#x53F0;&#xFF0C;&#x4E14;&#x8DDD;&#x672C;&#x6B21;&#x6253;&#x5F00;&#x65F6;&#x95F4;&#x8D85;&#x8FC7;&#x4E86;&#x8BBE;&#x7F6E;&#x7684;session
        timeout&#x65F6;&#x95F4;&#x65F6;&#xFF0C;&#x8BE5;&#x65F6;&#x95F4;&#x4F1A;&#x88AB;&#x89E6;&#x53D1;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x4E0A;&#x6B21;&#x8BBF;&#x95EE;&#x65F6;&#x957F;(Previous Session Length)</td>
      <td
      style="text-align:left"><code>a.PrevSessionLength</code>
        </td>
        <td style="text-align:left">&#x4E0A;&#x6B21;&#x5C0F;&#x7A0B;&#x5E8F;&#x6253;&#x5F00;&#xFF0C;&#x4E14;&#x5728;&#x524D;&#x53F0;&#x8FD0;&#x884C;&#x7684;&#x603B;&#x65F6;&#x957F;&#x3002;&#x4EE5;&#x79D2;&#x4E3A;&#x5355;&#x4F4D;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6253;&#x5F00;&#x6B21;&#x6570;(Launch Number)</td>
      <td style="text-align:left"><code>a.Launches</code>
      </td>
      <td style="text-align:left">&#x5C0F;&#x7A0B;&#x5E8F;&#x6253;&#x5F00;&#xFF0C;&#x6216;&#x8005;&#x4ECE;&#x540E;&#x53F0;&#x88AB;&#x5524;&#x9192;&#x81F3;&#x524D;&#x53F0;&#x7684;&#x6B21;&#x6570;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x8DDD;&#x9996;&#x6B21;&#x6253;&#x5F00;&#x5929;&#x6570;(Days since first
        use)</td>
      <td style="text-align:left"><code>a.DaysSinceFirstUse</code>
      </td>
      <td style="text-align:left">&#x8DDD;&#x7B2C;&#x4E00;&#x6B21;&#x8FD0;&#x884C;&#x8BE5;&#x5C0F;&#x7A0B;&#x5E8F;&#x7684;&#x5929;&#x6570;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x8DDD;&#x4E0A;&#x6B21;&#x6253;&#x5F00;&#x5929;&#x6570;(Days since last
        use)</td>
      <td style="text-align:left"><code>a.DaysSinceLastUse</code>
      </td>
      <td style="text-align:left">&#x8DDD;&#x4E0A;&#x4E00;&#x6B21;&#x8FD0;&#x884C;&#x8BE5;&#x5C0F;&#x7A0B;&#x5E8F;&#x7684;&#x5929;&#x6570;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x6253;&#x5F00;&#x65F6;&#x70B9;</p>
        <p>(Hour of Day)</p>
      </td>
      <td style="text-align:left"><code>a.HourOfDay</code>
      </td>
      <td style="text-align:left">&#x8BB0;&#x5F55;&#x5C0F;&#x7A0B;&#x5E8F;&#x6253;&#x5F00;&#x65F6;&#x7684;&#x6574;&#x70B9;&#x503C;&#xFF0C;&#x4EE5;24&#x5C0F;&#x65F6;&#x5F62;&#x5F0F;&#x8BA1;&#x65F6;&#x3002;&#x53EF;&#x7528;&#x8BE5;&#x6307;&#x6807;&#x6765;&#x6D4B;&#x7B97;&#x5C0F;&#x7A0B;&#x5E8F;&#x7684;&#x9AD8;&#x5CF0;&#x4F7F;&#x7528;&#x65F6;&#x70B9;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x6253;&#x5F00;&#x65E5;</p>
        <p>(Day of Week)</p>
      </td>
      <td style="text-align:left"><code>a.DayOfWeek</code>
      </td>
      <td style="text-align:left">&#x8BB0;&#x5F55;&#x5C0F;&#x7A0B;&#x5E8F;&#x5728;&#x4E00;&#x5468;&#x4E2D;&#x7684;&#x54EA;&#x4E00;&#x5929;&#x6253;&#x5F00;&#x3002;</td>
    </tr>
  </tbody>
</table>

### Device information

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x6307;&#x6807;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x6807;&#x8BC6;&#x7B26;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">AppID</td>
      <td style="text-align:left"><code>a.AppID</code>
      </td>
      <td style="text-align:left">&#x7528;&#x4E8E;&#x4FDD;&#x5B58;&#x5C0F;&#x7A0B;&#x5E8F;&#x540D;&#x79F0;&#x53CA;&#x7248;&#x672C;&#x3002;&#x683C;&#x5F0F;&#x4E3A;&#xFF1A;<code>AppName BundleVersion (app version code)&#x3002;</code>&#x4F8B;&#x5982;&#xFF1A;<code>MyAppName 1.1(1)&#x3002;</code>&#x8BE5;&#x503C;&#x6765;&#x81EA;&#x4E8E;SDK&#x521D;&#x59CB;&#x5316;&#x8BBE;&#x7F6E;&#x4E2D;&#x7684;<code>app.id&#x3002;</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x8BBE;&#x5907;&#x540D;&#x79F0;(Device Name)</td>
      <td style="text-align:left"><code>a.DeviceName</code>
      </td>
      <td style="text-align:left">&#x7528;&#x4E8E;&#x4FDD;&#x5B58;&#x8BBE;&#x5907;&#x540D;&#x79F0;&#x3002;&#x4F8B;&#x5982;&#xFF1A;iphone
        5</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x64CD;&#x4F5C;&#x7CFB;&#x7EDF;&#x53CA;&#x7248;&#x672C;(Operation system
        version)</td>
      <td style="text-align:left"><code>a.OSVersion</code>
      </td>
      <td style="text-align:left">&#x7528;&#x4E8E;&#x4FDD;&#x5B58;&#x64CD;&#x4F5C;&#x7CFB;&#x7EDF;&#x540D;&#x79F0;&#x4EE5;&#x53CA;&#x7248;&#x672C;&#x4FE1;&#x606F;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x5206;&#x8FA8;&#x7387;</p>
        <p>(Resolution)</p>
      </td>
      <td style="text-align:left"><code>a.Resolution</code>
      </td>
      <td style="text-align:left">&#x5C4F;&#x5E55;&#x7684;&#x5206;&#x8FA8;&#x7387;&#xFF0C;&#x5355;&#x4F4D;&#x662F;&#x50CF;&#x7D20;&#x3002;&#x4F8B;&#x5982;&#xFF1A;456
        x 320</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x8FD0;&#x884C;&#x6A21;&#x5F0F;</p>
        <p>(Run mode)</p>
      </td>
      <td style="text-align:left"><code>a.RunMode</code>
      </td>
      <td style="text-align:left">&#x8FD0;&#x884C;&#x6A21;&#x5F0F;&#x3002;&#x8BE5;&#x503C;&#x4E3A;&quot;Application&quot;&#x3002;</td>
    </tr>
  </tbody>
</table>

## 验证发送给Analytics的请求

以下为向Analytics发送请求的示例。

### 生命周期指标 - 小程序安装

```text
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&InstallEvent=InstallEvent&InstallDate=6%2F17%2F2019&LaunchEvent=LaunchEvent&PrevSessionLength=0&Launches=1&DaysSinceFirstUse=0&DaysSinceLastUse=0&MonthlyEngUserEvent=MonthlyEngUserEvent&DailyEngUserEvent=DailyEngUserEvent&HourOfDay=14&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.2)&aid=56025F971A9133B0-064362B2442D266E&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560802302&cp=foreground
```

### 生命周期指标 - 小程序打开

```text
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.1)&LaunchEvent=LaunchEvent&PrevSessionLength=8&Launches=4&DaysSinceFirstUse=0&DaysSinceLastUse=0&HourOfDay=11&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.1)&aid=5B2BF542EAE66678-0E94474822B39961&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560792653&cp=foreground
```

### 生命周期指标 - 小程序升级

```text
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&UpgradeEvent=UpgradeEvent&DaysSinceLastUpgrade=0&LaunchesSinceUpgrade=1&LaunchEvent=LaunchEvent&PrevSessionLength=3&Launches=2&DaysSinceFirstUse=0&DaysSinceLastUse=0&HourOfDay=11&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.2)&aid=230EDCDE65A436D6-05BCD5A3D1105CA4&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560792765&cp=foreground
```

### TrackAction

```text
ndh=1&c.&a.&OSVersion=Android%205.0&DeviceName=Nexus%206&Resolution=610x412&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&action=Start&.a&example.&key=value&.example&.c&pe=lnk_o&pev2=AMACTION%3AStart&pageName=adobe-demo%20(0.0.0.2)&aid=2E85DEB17FFF8000-52245FFFDDC6DB5D&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1561063668&cp=foreground
```

### TrackState

```text
ndh=1&c.&a.&OSVersion=Android%205.0&DeviceName=Nexus%206&Resolution=610x412&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&action=&TimeSinceLaunch=0&.a&.c&pageName=HomePage&aid=2E85DEB17FFF8000-52245FFFDDC6DB5D&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1561063668&cp=foreground
```

## 观看视频

{% embed url="https://video.tv.adobe.com/v/28355t1/?quality=9" %}

### 

