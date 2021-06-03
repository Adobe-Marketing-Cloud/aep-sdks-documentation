# Implementation

{% hint style="warning" %}
While the Adobe Experience Platform SDK for WeChat Mini Programs is complimentarily available for all Adobe customers, the SDK for the WeChat Mini Program requires _in-country_ data collection.

Customers must purchase the _China Performance Optimization Add-On_ for Adobe Analytics in order to use the SDK. Please contact your Adobe account team for further detail.
{% endhint %}

To implement the Adobe Experience Platform SDK in your WeChat Mini Programs, complete the following steps:

## 1. Add the SDK to your project

In your Mini Program's `app.js` file, you can add the SDK by copying the following example:

```javascript
const AdobeSDK = require('AdobeSDK.js');
```

## 2. Initialize the SDK

In the `onLaunch` method of your `app.js` file, implement `AdobeSDK.init()` and pass in valid configuration values using the **.init\(configuration\)** method. An example of that can be seen below:

{% hint style="warning" %}
If you need help to find the settings for your Adobe Analytics implementation, contact your Adobe Analytics administrator or Adobe consulting.
{% endhint %}

```javascript
// App({
//   onLaunch: function () {
//     // 展示本地存储能力
//     var logs = wx.getStorageSync('logs') || []
//     logs.unshift(Date.now())
//     wx.setStorageSync('logs', logs)
     AdobeSDK.init({
       "analytics.server": "example.sc.adobedc.cn",      //required
       "analytics.rsids": "example.reportsuite",    //required
       "app.id": "adobe-demo",                        //required
       "app.version": "0.0.0.1",           //optional, default value = ''
       "analytics.offlineEnabled": true,   //optional, default value = false
       "session.timeout": 30               //optional, default value = 30
     });
// })
```

{% hint style="info" %}
If the key `analytics.offlineEnabled` is set to true, then `timestamp(ts)` is included in the Adobe Analytics request.

The key `lifecycle.sessionTimeout` represents the period, in seconds, that must elapse between the time the app is launched and before the launch is considered to be a new session. This timeout also applies when your application is sent to the background and reactivated. The default value is 30 seconds.

To send data to multiple report suites, use commas to separate RSIDs in the configuration code block. For example: `"analytics.rsids": "example.rsid1,example.rsid2"` causes the SDK to send data to the `example.rsid1` and `example.rsid2` report suites.
{% endhint %}

{% hint style="success" %}
After being initialized, the SDK automatically collects and transmits lifecycle metrics to Adobe Analytics. For a complete list of metrics, please read the document on [Lifecycle metrics](implementation.md#lifecycle-metrics).
{% endhint %}

## 3. Enable debug logging

### AdobeSDK.setDebugLoggingEnabled\(flag\)

```javascript
AdobeSDK.setDebugLoggingEnabled(true)
```

### AdobeSDK.setDebugModeEnabled\(flag\)

By default, the SDK hides internal exceptions and prints error message in the console log. To allow the SDK to throw those exceptions, enable debug mode.

```javascript
AdobeSDK.setDebugModeEnabled(true)
```

## 4. Track screens and user actions

You can use the following screen and action tracking APIs to measure your user's engagement with your app.

### AdobeSDK.trackAction\(actionName, contextData\)

Actions are events that occur in your app. Use this API to track and measure an action, where each action has one or more corresponding metrics that increment each time the event occurs. For example, you can call this API for every new subscription, every time an article is viewed, or every time a level is completed.

{% hint style="info" %}
`trackAction` reports the action as an **event** and does not increment your page views in Analytics. The value is sent to Analytics by using the action variable (`action=value`).
{% endhint %}

```javascript
AdobeSDK.trackAction("action", { "example.key": "value" });
```

### AdobeSDK.trackState(stateName, contextData)

{% hint style="info" %}
In Analytics, `trackState` reports the view state as the **Page Name**, and state views are reported as the **Page View**. The value is sent to Adobe Analytics by using the page name variable (`pagename=value`).

To track when users switch to screens or pages, implement this API in the `onShow` method of the `Page`.
{% endhint %}

```javascript
AdobeSDK.trackState("state", { "example.key": "value" });
```

## Lifecycle metrics

After the SDK is initialized, Lifecycle metrics are automatically sent to Adobe Analytics. A complete list of the metrics that are collected and sent can be found below:

### Install <a id="install"></a>

| **Metric** | **Key** | **DescriptIon** |
| :--- | :--- | :--- |
| First Launches | `a.InstallEvent` | Triggered at first run after installation or re-installation. |
| Install Date | `a.InstallDate` | Date of first launch after installation. The format is `M/d/yyyy`, and an example is `5/3/2017`. |

### Upgrade

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Upgrades | `a.UpgradeEvent` | Triggered at the first run after upgrade or when the version number changes. |
| Days since last upgrade | `a.DaysSinceLastUpgrade` | Number of days since the application version number  changed. |
| Launches since last upgrade | `a.LaunchesSinceUpgrade` | Number of launches since the application version number changed. |

### Launch

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Daily Engaged Users | `a.DailyEngUserEvent` | Triggered when the application is used on a particular day. **Important**: This metric is **not** automatically stored in Adobe Analytics. You must create a processing rule that sets a custom event to capture this metric. |
| Monthly Engaged Users | `a.MonthlyEngUserEvent` | Triggered when the application is used during a particular month. **Important**: This metric is **not** automatically stored in Analytics. You must create a processing rule that sets a custom event to capture this metric. |
| Launches | `a.LaunchEvent` | Triggered on every run, including crashes and installs. This value is also triggered when the app is resumed from the background after the lifecycle session timeout is exceeded. |
| Previous Session Length | `a.PrevSessionLength` | Reports the number of seconds that a previous application session lasted, based on how long the application was open and in the foreground. |
| Launch Number | `a.Launches` | The number of times the application was launched or brought out of the background. |
| Days since first use | `a.DaysSinceFirstUse` | Number of days since the first run. |
| Days since last use | `a.DaysSinceLastUse` | Number of days since the last use. |
| Hour of Day | `a.HourOfDay` | Measures the hour the app was launched and uses the 24-hour numerical format. Used for time parting to determine peak usage times. |
| Day of Week | `a.DayOfWeek` | Measures the day of the week the app was launched. |

### Device information

| Metric | Key | Description |
| :--- | :--- | :--- |
| AppID | `a.AppID` | Stores the application name and version in the `AppName BundleVersion (app version code)` format. An example of this format is `MyAppName 1.1(1)`. This value will be populated from the app ID provided in the SDK configuration. |
| .Device name | `a.DeviceName` | Stores the device name. |
| Operating system version | `a.OSVersion` | Operating system name and version. |
| Resolution | `a.Resolution` | Width x height, in pixels. |
| Run mode | `a.RunMode` | The SDK running mode, for example, `Application/Extension`. |

## 5. Validate requests to Adobe Analytics

The following blurbs shows example of Adobe Analytics hits:

### Lifecycle - Install Event

```text
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&InstallEvent=InstallEvent&InstallDate=6%2F17%2F2019&LaunchEvent=LaunchEvent&PrevSessionLength=0&Launches=1&DaysSinceFirstUse=0&DaysSinceLastUse=0&MonthlyEngUserEvent=MonthlyEngUserEvent&DailyEngUserEvent=DailyEngUserEvent&HourOfDay=14&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.2)&aid=56025F971A9133B0-064362B2442D266E&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560802302&cp=foreground
```

### Lifecycle - Launch Event

```text
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.1)&LaunchEvent=LaunchEvent&PrevSessionLength=8&Launches=4&DaysSinceFirstUse=0&DaysSinceLastUse=0&HourOfDay=11&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.1)&aid=5B2BF542EAE66678-0E94474822B39961&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560792653&cp=foreground
```

### Lifecycle - Upgrade Event

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

## Watch the video

For more information about WeChat Mini Programs SDK, watch the following video:

{% embed url="https://video.tv.adobe.com/v/28355t1/?quality=9" caption="" %}

