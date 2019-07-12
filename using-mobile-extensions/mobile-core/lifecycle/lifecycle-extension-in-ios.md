# Lifecycle extension in iOS

{% hint style="warning" %}
In version 4 of the iOS SDK, this implementation was completed automatically.

When upgrading to the Experience Platform SDK, you must add code to continue collecting Lifecycle metrics.

For more information, see [Manual Lifecycle Implementation](../../resources/upgrading-to-aep/manual-lifecycle-implementation.md).
{% endhint %}

You can track lifecycle to learn how frequently and how long your app is being used.

**Tip:** The code snippets in this section are only examples. Your final implementation will probably contain additional code that is specific to your app.

**Important**: The Lifecycle extension supports the `lifecycleStart:` and `lifecyclePause` APIs from the `ACPCore` extension to track application lifecycle for the Adobe SDK.

### Implementing Lifecycle metrics in iOS

After you enable lifecycle, each time your app is launched, one hit is sent to measure launches, upgrades, sessions, engaged users, and many other metrics.

To implement lifecycle metrics, complete the following steps:

1. Import the library:

   ```objectivec
   #import "ACPLifecycle.h"
   #import "ACPCore.h"
   ```

2. Register the Lifecycle extension: In your app's `didFinishLaunchingWithOptions` function register the Lifecycle extensions.

   ```objectivec
   - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
       [ACPLifecycle registerExtension];

       // Override point for customization after application launch.
       return YES;
   }
   ```

## APIs

Here are the APIs for the Lifecycle extension:

#### Lifecycle Start

The `lifecycleStart:` method tells the SDK that the user is launching the app. It should be called from both entry points in your `AppDelegate`:

* `application:didFinishLaunchingWithOptions:`  
* `applicationWillEnterForeground:`

Here are code samples for `lifecycleStart` in Objective-C and Swift:

**Objective-C**

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // optionally pass in additional lifecycle data as a dictionary parameter in this call
    [ACPCore lifecycleStart:nil];

    return YES;
}

- (void)applicationWillEnterForeground:(UIApplication *)application {
    // additional lifecycle data may also be passed here!
    [ACPCore lifecycleStart:nil];
}
```

**Swift**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
    ACPCore.lifecycleStart(nil)
    return true
}

func applicationWillEnterForeground(_ application: UIApplication) {
    ACPCore.lifecycleStart(nil)
}
```

#### Lifecycle Pause

The SDK needs to know when your app has entered the background to properly calculate your lifecycle metrics. The `lifecyclePause` method should be called when your user naturally backgrounds your application, in the `applicationDidEnterBackground:` method.

Here are some examples for `lifecyclePause` in Objective-C and Swift:

**Objective-C**

```objectivec
- (void) applicationDidEnterBackground:(UIApplication *)application {
    [ACPCore lifecyclePause];
}
```

**Swift**

```swift
func applicationDidEnterBackground(_ application: UIApplication) {    
    ACPCore.lifecyclePause()
}
```

### Tracking App Crashes in iOS

This information helps you understand how crashes are tracked and the best practices to handle false crashes.

**Important**: You should upgrade to Adobe Experience Platform SDKs, which contains critical changes that prevent false crashes from being reported.

**When does Adobe report a crash?**

If your application is terminated without having first been backgrounded, the SDK reports a crash the next time your app is launched.

**What can cause a false crash to be reported?**

The following scenarios are known to falsely cause a crash to be reported by the SDK:

* If you are debugging using Xcode, launching the app again while it is in the foreground, causes a crash.

  **Tip:** You can avoid a crash in this scenario by backgrounding the app before launching the app again from Xcode.

* If your app is in the background and sends Analytics hits through a call other than `trackActionFromBackground`, `trackLocation`, or `trackBeacon`, and the app is terminated \(manually or by the operating system\) while in the background, and the next launch will be a crash.

**Tip:** Background activity that occurs beyond the `lifecycleTimeout` threshold might also result in an additional false launch.

* If your app is launched in the background because of a background fetch, location update, and so on, and is terminated by the operating without coming to the foreground, the next launch \(background or foreground\) results in a crash.
* If you programmatically delete Adobe’s pause flag from `NSUserDefaults`, while the app is in the background, the next launch or resume causes a crash.

**How can I prevent false crashes from being reported?**

The following practices can help prevent false crashes from being reported:

* Ensure that you perform your development against non-production report suites, which should prevent false crash from the first bullet point from occurring.
* Do not delete or modify any values that the Experience Platform SDKs puts in `NSUserDefaults`.  If these values are modified outside the SDK, the data reported will be invalid.

**How does crash reporting work?**

iOS uses system notifications that allow developers to track and respond to different states and events in the application lifecycle. The Experience Platform SDKs has a notification handler that responds to the `UIApplicationDidEnterBackgroundNotification` notification. In this code, a value is set that indicates that the user has backgrounded the app. On a subsequent launch, if that value cannot be found, a crash is reported.

**Why does Adobe measure crashes this way?**

This approach of measuring crashes provides a high-level answer to the question, Did the user exit my app intentionally? Crash reporting libraries provided by companies such as Apteligent \(formerly Crittercism\) use a global `NSException` handler to provide more detailed crash reporting. Your app is not allowed to have more than one of these kinds of handlers. Adobe decided to not implement a global `NSException` handler to prevent build errors, knowing that our customers might be using other crash reporting providers.

### Collecting Additional Data with Lifecycle

When calling `lifecycleStart:`, you can optionally pass a dictionary of additional data that will be attached to the lifecycle event.

**Tip**: You can pass additional data to lifecycle on app launch, app resume, both, or neither.

```objectivec
// Objective-C
- (void) applicationWillEnterForeground:(UIApplication *)application {      
    [ACPCore lifecycleStart:@{@"state": @"appResume"}];      
}
```

```swift
// Swift
func applicationWillEnterForeground(_ application: UIApplication) {      
    ACPCore.lifecycleStart(["state": "appResume"])
}
```
