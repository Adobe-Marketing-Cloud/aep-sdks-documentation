# WeChat Mini Programs

The Adobe Experience Platform SDK for WeChat Mini Programs brings Adobe Experience Cloud & Adobe Experience Platform functionality to developers building Mini Programs. The scope for the beta and the subsequent general release will be for Adobe Analytics customers who want to track behavioral usage of branded Mini Programs.

{% hint style="warning" %}
This functionality is currently in beta. Contact your Adobe account representatives or CSM to learn more and participate in this beta.
{% endhint %}

## Features

* Pass in the configuration, including Analytics and app-related settings.
* Send Analytics track action/state call.
* Collect `lifecycle` data, including launch, install, upgrade events, and previous session length.
* Use `aid` to identify a unique user.
  * \(Android\) Retrieve `aid` from remote Analytics server at the first app launch. 
  * \(iOS\) Generate `aid` locally at the first app launch.
  * Store `aid` and Lifecycle-related data into local storage.
* Use a `queue` to guarantee the request are being sent in order, which avoids occupying multiple HTTP requests quota.
* Enable or disable debug logging.
* Enable or disable debug mode.

## Using the Mobile SDK in the Mini Program SDK

1. In the `onLaunch` method of the `App.js`, implement `AdobeSDK.init()` and pass in valid configurations.
2. Enable debug logging if needed.
3. Call `AdobeSDK.trackState()` when you switch to a new `Page`  pass in the page name and any additional context data.   You can usually implement this in the `onShow` method of the `Page`.
4. To track a certain event, call `AdobeSDK.trackAction()` .

## Public API

Here are the public APIs in the Mini ProgramS SDK:

### AdobeSDK.init\(configurations\)

```javascript
AdobeSDK.init({
      "analytics.server": "test.sc.adobedc.cn",      //required
      "analytics.rsids": "mobile5wechat.explore",    //required
      "app.id": "adobe-demo",                        //required
      "app.version": "0.0.0.1",                      //optional, default value = ''
      "analytics.offlineEnabled": true,              //optional, default value = false
      "session.timeout": 30                          //optional, default value = 30
    });
```

If this config is enabled, The `analytics.offlineEnabled` timestamp\(ts\) is included in Analytics request .

### AdobeSDK.setDebugLoggingEnabled\(flag\)

```javascript
AdobeSDK.setDebugLoggingEnabled(true)
```

### AdobeSDK.setDebugModeEnabled\(flag\)

By default, the SDK swallows internal exceptions and print error message in console log. To let the SDK throw those exceptions, you need to enable debug mode.

```javascript
AdobeSDK.setDebugModeEnabled(true)
```

### AdobeSDK.trackAction\(actionName, contextData\)

```javascript
AdobeSDK.trackAction("action", { "example.key": "value" });
```

### AdobeSDK.trackState\(stateName, contextData\)

```javascript
AdobeSDK.trackState("state", { "example.key": "value" });
```

### Analytics hits example

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

