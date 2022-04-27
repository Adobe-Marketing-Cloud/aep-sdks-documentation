# Manual Lifecycle Implementation

In the Experience Platform SDK, all Lifecycle implementation must be done manually. This page provides a suggested implementation of Lifecycle. The correct implementation for Lifecycle should ultimately be determined by the app developer.

{% hint style="danger" %}
In version 4 of the iOS SDK, this implementation was completed automatically.

When upgrading to the Experience Platform SDK, you must add code to continue collecting Lifecycle metrics.
{% endhint %}

## Importing and registering the Lifecycle extension

{% tabs %}
{% tab title="Android" %}
### Java

Import the Lifecycle framework:

```java
import com.adobe.marketing.mobile.*;
```

Register the framework with Mobile Core:

```java
public class MyApp extends Application {​

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);

        try {
            Lifecycle.registerExtension();
        } catch (Exception e) {
            // Log the exception
        }
    }
}
```
{% endtab %}

{% tab title="iOS" %}
### Objective-C

Import the Lifecycle framework:

```objectivec
#import "ACPLifecycle.h"
```

Register the Lifecycle extension with the SDK Core by adding the following to your app's `application:didFinishLaunchingWithOptions:` delegate method:

```objectivec
- (BOOL) application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // register the lifecycle extension
    [ACPLifecycle registerExtension];
}
```

### Swift

In Swift, importing `ACPCore` also imports the necessary Lifecycle APIs:

```swift
import ACPCore
```

Register the Lifecycle extension with the SDK Core by adding the following in your app's `application:didFinishLaunchingWithOptions:` delegate method:

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // register the lifecycle extension
    ACPLifecycle.registerExtension();
}
```
{% endtab %}

{% endtabs %}

## Start collecting Lifecycle information

You can start collecting Lifecycle information at any time in your app, but we recommend that you start as soon as your app enters the foreground. This allows Lifecycle metrics to be correctly attributed to all of your users' activities for their current session.

{% tabs %}
{% tab title="Android" %}
### Java

{% hint style="danger" %}
Do not start or stop Lifecycle in a Fragment.
{% endhint %}

In the `onResume` function of each of your Activities, start Lifecycle data collection:

```java
@Override  
public void onResume() {  
    MobileCore.setApplication(getApplication());
    MobileCore.lifecycleStart(null);
}
```

{% hint style="warning" %}
To ensure accurate session and crash reporting, this call must be added to every Activity.
{% endhint %}

{% hint style="info" %}
Setting the application is only necessary on activities that are entry points for your application. However, setting the application on each Activity has no negative impact and ensures that the SDK always has the necessary reference to your application. We recommend that you call `setApplication` in each of your Activities.
{% endhint %}
{% endtab %}

{% tab title="iOS" %}
### Objective-C

Start Lifecycle data collection by calling `lifecycleStart:` from within the callback of the `ACPCore::start:` method in your app's `application:didFinishLaunchingWithOptions:` delegate method.

{% hint style="warning" %}
If your iOS application supports background capabilities, your `application:didFinishLaunchingWithOptions:` method might be called when iOS launches your app in the background. If you do not want background launches to count towards your lifecycle metrics, `lifecycleStart:` should only be called when the application state is not equal to `UIApplicationStateBackground`.
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

When your app is launched, if it is resuming from a backgrounded state, iOS might call your `applicationWillEnterForeground:` delegate method. You also need to call `lifecycleStart:`, but this time you do not need all of the supporting code that you used in `application:didFinishLaunchingWithOptions:`:

```objectivec
- (void) applicationWillEnterForeground:(UIApplication *)application {
    [ACPCore lifecycleStart:nil];
}
```

If your app is a SceneDelegate based iOS application, then use:

```objective-c
- (void) sceneWillEnterForeground:(UIScene *)scene {
    [ACPCore lifecycleStart:nil];
}
```

### Swift

Start Lifecycle data collection by calling `lifecycleStart:` from the callback of the `ACPCore::start:` method in your app's `application:didFinishLaunchingWithOptions:` delegate method.

{% hint style="warning" %}
If your iOS application supports background capabilities, your `application:didFinishLaunchingWithOptions:` method might be called when iOS launches your app in the background. If you do not want background launches to count towards your lifecycle metrics, `lifecycleStart:` should only be called when the application state is not equal to `UIApplicationStateBackground`.
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

When your app is launched, if it is resuming from a backgrounded state, iOS might call your `applicationWillEnterForeground:` delegate method. You also need to call `lifecycleStart:`, but this time you do not need all of the supporting code that you used in `application:didFinishLaunchingWithOptions:`:

```swift
func applicationWillEnterForeground(_ application: UIApplication) {    
    ACPCore.lifecycleStart(nil)
}
```
If your app is a SceneDelegate based iOS application, then use:

```swift
 func sceneWillEnterForeground(_ scene: UIScene) {
      ACPCore.lifecycleStart(nil)
 }
```

{% endtab %}

{% endtabs %}

## Pause Lifecycle Collection

You should pause Lifecycle collection when the user stops using your app. The best time to do this is usually when your app has entered the background.

{% tabs %}
{% tab title="Android" %}
### Java

{% hint style="danger" %}
Do not start or stop Lifecycle in a Fragment.
{% endhint %}

We recommend pausing Lifecycle from the `onPause` function in your Activities:

```java
@Override
public void onPause() {
    MobileCore.lifecyclePause();
}
```

{% hint style="warning" %}
To ensure accurate session and crash reporting, this call must be added to every Activity.
{% endhint %}
{% endtab %}

{% tab title="iOS" %}
### Objective-C

When the app enters the background, pause Lifecycle data collection from your app's `applicationDidEnterBackground:` delegate method:

```objectivec
 - (void) applicationDidEnterBackground:(UIApplication *)application {
    [ACPCore lifecyclePause];
 }
```

If your app is a SceneDelegate based iOS application, then use:

```objective-c
- (void) sceneDidEnterBackground:(UIScene *)scene {
    [ACPCore lifecyclePause];
}
```

### Swift

When the app enters the background, pause Lifecycle data collection from your app's `applicationDidEnterBackground:` delegate method:

```swift
func applicationDidEnterBackground(_ application: UIApplication) {    
    ACPCore.lifecyclePause()
}
```
If your app is a SceneDelegate based iOS application, then use:

```swift
func sceneDidEnterBackground(_ scene: UIScene) {
     ACPCore.lifecyclePause()
 }
```

{% endtab %}

{% endtabs %}

For more information, see [Lifecycle Metrics](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/87ccee59e0aeb622ec110a51820006b4a688a059/resources/using-mobile-extensions/mobile-core/lifecycle/README.md).

