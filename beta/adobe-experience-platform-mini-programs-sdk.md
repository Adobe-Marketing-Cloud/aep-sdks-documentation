# Adobe Experience Platform Mini Programs SDK

## Features

* Pass in the configuration, including analytics and app related settings.
* Send Analytics track action/state call.
* Collect `lifecycle` data, including launch/install/upgrade events, and previous session length.
* Use `aid` to identify a unique user.
  * Retrieve `aid` from remote analytics server at the first app launch. \(Android\).
  * Generate `aid` locally at the first app launch. \(iOS\).
  * Store `aid` and Lifecycle related data into local storage.
* Use a `queue` to guarantee the request are being sent in order, also to avoid occupying multiple HTTP requests quota.
* Enable or disable debug logging.
* Enable or disable debug mode.

## Using Mobile SDK in WeChat Mini Program

1. In the `onLaunch` method of the `App.js`, implement `AdobeSDK.init()`, and pass in valid configurations.
2. Enable debug logging if needed.
3. Call `AdobeSDK.trackState()` when switch to a new `Page`, and pass in the page name and any additional context data.  Normally, you can implement this in the `onShow` method of the `Page`.
4. To track a certain event, call `AdobeSDK.trackAction()` .

## Public API

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

The `analytics.offlineEnabled` timestamp\(ts\) will be included in Analytics request if this config is enabled.

### AdobeSDK.setDebugLoggingEnabled\(flag\)

```javascript
AdobeSDK.setDebugLoggingEnabled(true)
```

### AdobeSDK.setDebugModeEnabled\(flag\)

By default, the SDK will swallow internal exceptions and print error message in console log. If you want to let the SDK throw those exceptions, you need to enable debug mode.

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

Here is a list of the Analytics hits for manual tests:

#### Lifecycle - Install Event

```javascript
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&InstallEvent=InstallEvent&InstallDate=6%2F17%2F2019&LaunchEvent=LaunchEvent&PrevSessionLength=0&Launches=1&DaysSinceFirstUse=0&DaysSinceLastUse=0&MonthlyEngUserEvent=MonthlyEngUserEvent&DailyEngUserEvent=DailyEngUserEvent&HourOfDay=14&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.2)&aid=56025F971A9133B0-064362B2442D266E&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560802302&cp=foreground
```

#### Lifecycle - Launch Event

```javascript
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.1)&LaunchEvent=LaunchEvent&PrevSessionLength=8&Launches=4&DaysSinceFirstUse=0&DaysSinceLastUse=0&HourOfDay=11&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.1)&aid=5B2BF542EAE66678-0E94474822B39961&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560792653&cp=foreground
```

#### Lifecycle - Upgrade Event

```javascript
ndh=1&c.&a.&OSVersion=iOS%2010.0.1&DeviceName=iPhone%207&Resolution=555x375&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&UpgradeEvent=UpgradeEvent&DaysSinceLastUpgrade=0&LaunchesSinceUpgrade=1&LaunchEvent=LaunchEvent&PrevSessionLength=3&Launches=2&DaysSinceFirstUse=0&DaysSinceLastUse=0&HourOfDay=11&DayOfWeek=2&action=Lifecycle&TimeSinceLaunch=0&.a&.c&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&pageName=adobe-demo%20(0.0.0.2)&aid=230EDCDE65A436D6-05BCD5A3D1105CA4&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1560792765&cp=foreground
```

#### TrackAction

```javascript
ndh=1&c.&a.&OSVersion=Android%205.0&DeviceName=Nexus%206&Resolution=610x412&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&action=Start&.a&example.&key=value&.example&.c&pe=lnk_o&pev2=AMACTION%3AStart&pageName=adobe-demo%20(0.0.0.2)&aid=2E85DEB17FFF8000-52245FFFDDC6DB5D&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1561063668&cp=foreground
```

#### TrackState

```javascript
ndh=1&c.&a.&OSVersion=Android%205.0&DeviceName=Nexus%206&Resolution=610x412&RunMode=Application&PlatformVersion=wechat-6.6.3&AppId=adobe-demo%20(0.0.0.2)&action=&TimeSinceLaunch=0&.a&.c&pageName=HomePage&aid=2E85DEB17FFF8000-52245FFFDDC6DB5D&ce=UTF-8&t=00%2F00%2F0000%2000%3A00%3A00%200%20360&ts=1561063668&cp=foreground
```

### Next Steps

* Encrypt javascript code ???
* Npm moudule support
* Crash Event

