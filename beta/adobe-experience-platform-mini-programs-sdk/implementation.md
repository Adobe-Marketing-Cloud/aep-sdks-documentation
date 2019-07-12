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

## Enable debug logging

#### AdobeSDK.setDebugLoggingEnabled\(flag\)

```javascript
AdobeSDK.setDebugLoggingEnabled(true)
```

#### AdobeSDK.setDebugModeEnabled\(flag\)

By default, the SDK hides internal exceptions and print error message in console log. To let the SDK throw those exceptions, you need to enable debug mode.

```javascript
AdobeSDK.setDebugModeEnabled(true)
```

## Track screens and user actions

You may use the following screen and action tracking APIs to measure your user's engagement with your app.

#### AdobeSDK.trackAction\(actionName, contextData\)

Actions are events that occur in your app. Use this API to track and measure an action, where each action has one or more corresponding metrics that increment each time the event occurs. For example, you might call this API for each new subscription each time an article is viewed, or each time a level is completed.

{% hint style="info" %}
`trackAction`reports the Action as an **event** and does not increment your page views in Analytics. The value is sent to Analytics by using the action variable \(`action=value`\).
{% endhint %}

```javascript
AdobeSDK.trackAction("action", { "example.key": "value" });
```

#### AdobeSDK.trackState\(stateName, contextData\)

{% hint style="info" %}
`trackState` reports the View State as **Page Name**, and state views are reported as **Page View** in Analytics. The value is sent to Analytics by using the page name variable \(`pagename=value`\).
{% endhint %}

{% hint style="info" %}
This API may be implemented in the `onShow` method of the `Page`to track when users switch to screens or pages.
{% endhint %}

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

