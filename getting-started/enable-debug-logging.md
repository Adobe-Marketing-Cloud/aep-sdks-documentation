# Debugging & lifecycle metrics

## Debug logging

Debug logging is an optional, but a recommended and critical SDK feature.

By enabling logging, you can ensure that the SDK is working as intended. The following table explains levels of logging available and the purpose they serve:

| Log Level | Description |
| :--- | :--- |
| Error | This is the default log level used by SDK. This log level provides the details about unrecoverable errors that occurred during SDK implementation. |
| Warning | In addition to the details from _Error_ log level, _Warning_ provides error information during SDK integration. This log level might indicate that a request has been made to the SDK, but the SDK might be unable to perform the requested task. For example, this log level might be used when catching an unexpected, but recoverable, exception and printing its message. |
| Debug | In addition to the details from the _Warning_ log level, _Debug_ also provides high-level information about how the SDK processes network requests/responses data. |
| Verbose | In addition to the details from the _Debug_ level, _Verbose_ provides detailed, low-level information about how the SDK processes database interactions and SDK events. |

{% hint style="warning" %}
Using `Debug` or `Verbose` log levels may cause performance or security concerns. As a result, it is recommended that you use only `Error` or `Warning` log levels in production applications.
{% endhint %}

To enable debug logging, use the following methods:

{% tabs %}
{% tab title="Android" %}
## Java

```java
MobileCore.setLogLevel(LoggingMode.DEBUG);
// MobileCore.setLogLevel(LoggingMode.VERBOSE);
// MobileCore.setLogLevel(LoggingMode.WARNING);
// MobileCore.setLogLevel(LoggingMode.ERROR);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
## Swift

```swift
MobileCore.setLogLevel(.debug)
// MobileCore.setLogLevel(.trace)
// MobileCore.setLogLevel(.warning)
// MobileCore.setLogLevel(.error)
```

## Objective-C

```objectivec
[AEPMobileCore setLogLevel:AEPLogLevelDebug];
// [AEPMobileCore setLogLevel:AEPLogLevelTrace];
// [AEPMobileCore setLogLevel:AEPLogLevelWarning];
// [AEPMobileCore setLogLevel:AEPLogLevelError];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
## Objective-C

```objectivec
[ACPCore setLogLevel:ACPMobileLogLevelDebug];
// [ACPCore setLogLevel:ACPMobileLogLevelVerbose];
// [ACPCore setLogLevel:ACPMobileLogLevelWarning];
// [ACPCore setLogLevel:ACPMobileLogLevelError];
```

## Swift

```swift
ACPCore.setLogLevel(ACPMobileLogLevel.debug)
// ACPCore.setLogLevel(ACPMobileLogLevel.verbose)
// ACPCore.setLogLevel(ACPMobileLogLevel.warning)
// ACPCore.setLogLevel(ACPMobileLogLevel.error)
```
{% endtab %}

{% tab title="React Native" %}
## Javascript

```jsx
ACPCore.setLogLevel(ACPMobileLogLevel.DEBUG);
//ACPCore.setLogLevel(ACPMobileLogLevel.VERBOSE);
//ACPCore.setLogLevel(ACPMobileLogLevel.WARNING);
//ACPCore.setLogLevel(ACPMobileLogLevel.ERROR);
```
{% endtab %}

{% tab title="Flutter" %}
## Dart

```dart
FlutterACPCore.setLogLevel(ACPLoggingLevel.DEBUG);
//FlutterACPCore.setLogLevel(ACPLoggingLevel.VERBOSE);
//FlutterACPCore.setLogLevel(ACPLoggingLevel.WARNING);
//FlutterACPCore.setLogLevel(ACPLoggingLevel.ERROR);
```
{% endtab %}

{% tab title="Cordova" %}
## Cordova

```javascript
ACPCore.setLogLevel(ACPCore.ACPMobileLogLevelError, successCallback, errorCallback);
ACPCore.setLogLevel(ACPCore.ACPMobileLogLevelWarning, successCallback, errorCallback);
ACPCore.setLogLevel(ACPCore.ACPMobileLogLevelDebug, successCallback, errorCallback);
ACPCore.setLogLevel(ACPCore.ACPMobileLogLevelVerbose, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
## C\#

```csharp
ACPCore.SetLogLevel(ACPCore.ACPMobileLogLevel.ERROR);
ACPCore.SetLogLevel(ACPCore.ACPMobileLogLevel.WARNING);
ACPCore.SetLogLevel(ACPCore.ACPMobileLogLevel.DEBUG);
ACPCore.SetLogLevel(ACPCore.ACPMobileLogLevel.VERBOSE);
```
{% endtab %}
{% endtabs %}

## Lifecycle metrics

Lifecycle metrics are an optional, but valuable feature provided by the Adobe Experience Platform SDK. It provides out-of-the-box, application lifecycle information about your app user. A complete list of available metrics is provided in the [lifecycle documentation](../foundation-extensions/mobile-core/lifecycle/).

These metrics contain information on the app user's engagement lifecycle such as device information, install or upgrade information, and session start and pause times. You may also set additional lifecycle metrics.

{% hint style="warning" %}
This section shows you how to collect lifecycle metrics. To view, and report on this data in those respective solutions, you need to set up [Adobe Analytics](../using-mobile-extensions/adobe-analytics/) or other Experience Cloud solution extensions.
{% endhint %}

{% hint style="danger" %}
Lifecycle metrics are not available for Edge Network at this time. Check back soon on support for XDM-based lifecycle metrics for Edge Network implementations.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### Java

With the `onResume` function, start Lifecycle data collection:

```java
@Override  
   public void onResume() {  
      MobileCore.setApplication(getApplication());
      MobileCore.lifecycleStart(null);
   }
```

{% hint style="info" %}
Setting the application is only necessary on activities that are entry points for your application. However, setting the application on each `Activity` has no negative impact and ensures that the SDK always has the necessary reference to your application. As a result, you should call `setApplication` on each of your activities.
{% endhint %}

You can use the `onPause` function to pause the lifecycle data collection:

{% hint style="warning" %}
To ensure accurate session and crash reporting, this call must be added to every `Activity`.
{% endhint %}

```java
@Override
   public void onPause() {
      MobileCore.lifecyclePause();
   }
```
{% endtab %}

{% tab title="iOS - Objective-C" %}
### Objective-C

Start Lifecycle data collection by calling `lifecycleStart:` from within the callback of the `ACPCore::start:` method in your app's `application:didFinishLaunchingWithOptions:` delegate method.

{% hint style="warning" %}
If your iOS application supports background capabilities, you `application:didFinishLaunchingWithOptions:` method may be called when iOS launches your app in the background. If you do not want background launches to count towards your lifecycle metrics, then `lifecycleStart:` should only be called when the application state is not equal to `UIApplicationStateBackground`.
{% endhint %}

```objectivec
- (BOOL) application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // register the lifecycle extension
    [ACPLifecycle registerExtension];

    const UIApplicationState appState = application.applicationState;
    [ACPCore start:^{
        // only start lifecycle if the application is not in the background
        if (appState != UIApplicationStateBackground) {
            [ACPCore lifecycleStart:nil];
        }
    }];
}
```

When launched, if your app is resuming from a backgrounded state, iOS may call your `applicationWillEnterForeground:` delegate method. You also need to call `lifecycleStart:`, but this time you do not need all of the supporting code that you used in `application:didFinishLaunchingWithOptions:`:

```objectivec
- (void) applicationWillEnterForeground:(UIApplication *)application {
    [ACPCore lifecycleStart:nil];
}
```

When the app enters the background, pause Lifecycle data collection from your app's `applicationDidEnterBackground:` delegate method:

```objectivec
 - (void) applicationDidEnterBackground:(UIApplication *)application {
    [ACPCore lifecyclePause];
 }
```

### Swift

Start Lifecycle data collection by calling `lifecycleStart:` from within the callback of the `ACPCore::start:` method in your app's `application:didFinishLaunchingWithOptions:` delegate method.

{% hint style="warning" %}
If your iOS application supports background capabilities, your `application:didFinishLaunchingWithOptions:` method might be called when iOS launches your app in the background. If you do not want background launches to count towards your lifecycle metrics, then `lifecycleStart:` should only be called when the application state is not equal to `UIApplicationStateBackground`.
{% endhint %}

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
    // register the lifecycle extension
    ACPLifecycle.registerExtension();

    let appState = application.applicationState;            
    ACPCore.start {
        // only start lifecycle if the application is not in the background    
        if appState != .background {
            ACPCore.lifecycleStart(nil)
        }    
    }    
}
```

When launched, if your app is resuming from a backgrounded state, iOS might call your `applicationWillEnterForeground:` delegate method. You also need to call `lifecycleStart:`, but this time you do not need all of the supporting code that you used in `application:didFinishLaunchingWithOptions:`:

```swift
func applicationWillEnterForeground(_ application: UIApplication) {    
    ACPCore.lifecycleStart(nil)
}
```

When the app enters the background, pause Lifecycle data collection from your app's `applicationDidEnterBackground:` delegate method:

```swift
func applicationDidEnterBackground(_ application: UIApplication) {    
    ACPCore.lifecyclePause()
}
```
{% endtab %}

{% tab title="React Native" %}
## JavaScript

{% hint style="info" %}
You should implement Lifecycle metrics in native code. However, Lifecycle's APIs are available in Javascript if it fits your use case.
{% endhint %}

### Starting a Lifecycle event

```jsx
ACPCore.lifecycleStart({"lifecycleStart": "myData"});
```

### Pausing a Lifecycle event

```jsx
ACPCore.lifecyclePause();
```
{% endtab %}

{% tab title="Flutter" %}
## Flutter

{% hint style="info" %}
You need to implement Lifecycle in native Android and iOS code. For more information on implementing, please read the [Lifecycle documentation](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle).
{% endhint %}
{% endtab %}

{% tab title="Cordova" %}
## Cordova

{% hint style="info" %}
You need to implement Lifecycle in native Android and iOS code. For more information on implementing, please read the [Lifecycle documentation](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle).
{% endhint %}

**Getting Lifecycle version**

```javascript
ACPLifecycle.extensionVersion(function(version) {
    console.log(version);
}, function(error) {
    console.log(error);
});
```
{% endtab %}

{% tab title="Unity" %}
## C\#

### Starting and pausing a lifecycle event

```csharp
private void OnApplicationPause(bool pauseStatus)
{
  if (pauseStatus)
  {
    ACPCore.LifecyclePause();
  }
  else
  {
    var cdata = new Dictionary<string, string>();
    cdata.Add("launch.data", "added");
    ACPCore.LifecycleStart(cdata);
  }
}
```
{% endtab %}

{% tab title="Xamarin" %}
## C\#

**iOS**

### Starting and pausing a lifecycle event

```csharp
public override void WillEnterForeground(UIApplication uiApplication)
{
  base.WillEnterForeground(uiApplication);
  ACPCore.LifecycleStart(null);
}

public override void DidEnterBackground(UIApplication uiApplication)
{
  base.DidEnterBackground(uiApplication);
  ACPCore.LifecycleStart(null);
}
```

**Android**

### Starting and pausing a lifecycle event

```csharp
protected override void OnResume()
{
  base.OnResume();
  ACPCore.LifecycleStart(null);
}

protected override void OnPause()
{
  base.OnPause();
  ACPCore.LifecyclePause();
}
```
{% endtab %}
{% endtabs %}

For more information, see the documentation on [Lifecycle metrics](../foundation-extensions/mobile-core/lifecycle/).

