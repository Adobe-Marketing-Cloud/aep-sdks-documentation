# Implementation

The following instructions will help you implement the Adobe Experience Platform SDK in your WeChat Mini Programs.

{% hint style="danger" %}
**Getting the SDK**

Download links for the SDK will be provided as part of the beta welcome email, after the beta kick-off call. Please contact your Adobe account representative or CSM if you have not received this information.
{% endhint %}

## Add the SDK to your project

In your Mini Program's `app.js`file, reference and require the SDK, for example:

```javascript
const AdobeSDK = require('AdobeSDK.js');
```

1. Enable debug logging if needed.
2. Call `AdobeSDK.trackState()` when you switch to a new `Page`  pass in the page name and any additional context data.   You can usually implement this in the `onShow` method of the `Page`.
3. To track a certain event, call `AdobeSDK.trackAction()` .

## Initialize the SDK

In the `onLaunch` method of your `app.js` file, implement `AdobeSDK.init()` and pass in valid configuration values using the **.init\(configuration\)** method, for example:

```javascript
// App({
//   onLaunch: function () {
//     // 展示本地存储能力
//     var logs = wx.getStorageSync('logs') || []
//     logs.unshift(Date.now())
//     wx.setStorageSync('logs', logs)
     AdobeSDK.init({
       "analytics.server": "test.sc.adobedc.cn",      //required
       "analytics.rsids": "mobile5wechat.explore",    //required
       "app.id": "adobe-demo",                        //required
       "app.version": "0.0.0.1",           //optional, default value = ''
       "analytics.offlineEnabled": true,   //optional, default value = false
       "session.timeout": 30               //optional, default value = 30
     });
// })
```

{% hint style="info" %}
If analytics.offlineEnabled is set to true, then timestamp\(ts\) is included in Analytics request.
{% endhint %}

{% hint style="warning" %}
To find the right settings pertaining to Adobe Analytics implementation, contact your Adobe Analytics administrator or Adobe consulting for assistance.
{% endhint %}

## Implement SDK APIs

### Enable debug logging

#### AdobeSDK.setDebugLoggingEnabled\(flag\)

```javascript
AdobeSDK.setDebugLoggingEnabled(true)
```

#### AdobeSDK.setDebugModeEnabled\(flag\)

By default, the SDK hides internal exceptions and print error message in console log. To let the SDK throw those exceptions, you need to enable debug mode.

```javascript
AdobeSDK.setDebugModeEnabled(true)
```

### Tracking custom actions, events, and views

#### AdobeSDK.trackAction\(actionName, contextData\)

```javascript
AdobeSDK.trackAction("action", { "example.key": "value" });
```

#### AdobeSDK.trackState\(stateName, contextData\)

```javascript
AdobeSDK.trackState("state", { "example.key": "value" });
```

## Validate requests to Adobe Analytics

Here are the Analytics hits examples for manual tests:

#### Lifecycle - Install Event

```text
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&InstallEvent=InstallEvent&InstallDate=6%2F17%2F2019&LaunchEvent=LaunchEvent&PrevSessionLength=0&Launches=1&DaysSinceFirstUse=0&DaysSinceLastUse=0&MonthlyEngUserEvent=MonthlyEngUserEvent&DailyEngUserEvent=DailyEngUserEvent&HourOfDay=14&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.2)&aid=56025F971A9133B0-064362B2442D266E&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560802302&cp=foreground
```

#### Lifecycle - Launch Event

```text
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.1)&LaunchEvent=LaunchEvent&PrevSessionLength=8&Launches=4&DaysSinceFirstUse=0&DaysSinceLastUse=0&HourOfDay=11&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.1)&aid=5B2BF542EAE66678-0E94474822B39961&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560792653&cp=foreground
```

#### Lifecycle - Upgrade Event

```text
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&UpgradeEvent=UpgradeEvent&DaysSinceLastUpgrade=0&LaunchesSinceUpgrade=1&LaunchEvent=LaunchEvent&PrevSessionLength=3&Launches=2&DaysSinceFirstUse=0&DaysSinceLastUse=0&HourOfDay=11&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.2)&aid=230EDCDE65A436D6-05BCD5A3D1105CA4&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560792765&cp=foreground
```

#### TrackAction

```text
ndh=1&c.&a.&OSVersion=Android%205.0&DeviceName=Nexus%206&Resolution=610x412&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&action=Start&.a&example.&key=value&.example&.c&pe=lnk_o&pev2=AMACTION%3AStart&pageName=adobe-demo%20(0.0.0.2)&aid=2E85DEB17FFF8000-52245FFFDDC6DB5D&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1561063668&cp=foreground
```

#### TrackState

```text
ndh=1&c.&a.&OSVersion=Android%205.0&DeviceName=Nexus%206&Resolution=610x412&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&action=&TimeSinceLaunch=0&.a&.c&pageName=HomePage&aid=2E85DEB17FFF8000-52245FFFDDC6DB5D&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1561063668&cp=foreground
```

