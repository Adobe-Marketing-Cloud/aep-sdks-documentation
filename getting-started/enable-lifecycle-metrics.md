# Enable lifecycle metrics

{% hint style="warning" %}
This section shows you how to collect lifecycle metrics. To view, and report on this data in those respective solutions, you need to set up [Analytics](../using-mobile-extensions/adobe-analytics/) or other Experience Cloud solution extensions.
{% endhint %}

Lifecycle metrics is an optional, yet valuable feature provided by the Adobe Experience Platform SDK. It provides out-of-the-box, application lifecycle information about your app user. These metrics contain information on the app user's engagement lifecycle such as device information, install or upgrade information, session start and pause times, and so on. You can also set additional lifecycle metrics.

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
Setting the application is only necessary on activities that are entry points for your application. However, setting the application on each Activity has no negative impact and ensures that the SDK always has the necessary reference to your application. We recommend that you call `setApplication`in each of your activities.
{% endhint %}

You can use the `onPause` function to pause the lifecycle data collection:

{% hint style="warning" %}
To ensure accurate session and crash reporting, this call must be added to every activity.
{% endhint %}

```java
@Override
   public void onPause() {
      MobileCore.lifecyclePause();
   }
```
{% endtab %}

{% tab title="iOS" %}
### Objective-C

Start Lifecycle data collection by calling `lifecycleStart:` from within the callback of the `ACPCore::start:` method in your app's `application:didFinishLaunchingWithOptions:` delegate method.

{% hint style="warning" %}
If your iOS application supports background capabilities, your `application:didFinishLaunchingWithOptions:` method might be called when iOS launches your app in the background. If you do not want background launches to count towards your lifecycle metrics, then `lifecycleStart:` should only be called when the application state is not equal to `UIApplicationStateBackground`.
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

When launched, if your app is resuming from a backgrounded state, iOS might call your `applicationWillEnterForeground:` delegate method. You also need to call `lifecycleStart:`, but this time you do not need all of the supporting code that you used in `application:didFinishLaunchingWithOptions:`:

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

> Note: We recommend implementing Lifecycle metrics in native code, however, Lifecycle API's are available in Javascript if it fits your use case.

Starting a lifecycle event

```jsx
ACPCore.lifecycleStart({"lifecycleStart": "myData"});
```

Pausing a lifecycle event

```jsx
ACPCore.lifecyclePause();
```
{% endtab %}

{% tab title="Flutter" %}
## Flutter

Note: It is required to implement Lifecycle in native [Android and iOS code](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle).
{% endtab %}

{% tab title="Cordova" %}
## Cordova

> Note: We recommend implementing Lifecycle in native [Android and iOS code](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle).

**Getting Lifecycle version:**

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

Starting and pausing a lifecycle event

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

Starting and pausing a lifecycle event

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

Starting and pausing a lifecycle event

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

For more information, see [Lifecycle Metrics](../using-mobile-extensions/mobile-core/lifecycle/).

