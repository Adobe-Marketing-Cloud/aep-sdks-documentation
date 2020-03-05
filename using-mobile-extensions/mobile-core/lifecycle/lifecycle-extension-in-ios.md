# Lifecycle extension in iOS

{% hint style="warning" %}
In version 4 of the iOS SDK, this implementation was completed automatically.

When upgrading to the Experience Platform SDK, you must add code to continue collecting Lifecycle metrics. For more information, see [Manual Lifecycle Implementation](https://aep-sdks.gitbook.io/docs/resources/upgrading-to-aep/manual-lifecycle-implementation).
{% endhint %}

## Implementing Lifecycle metrics in iOS

For implementation details, please reference [Register Lifecycle with Mobile Core and Add Appropriate Start/Pause calls](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/db7da44a368ec6377ea0231078ffcae8a77491ab/using-mobile-extensions/lifecycle/README.md#register-lifecycle-with-mobile-core-and-add-appropriate-start-pause-calls).

## Tracking app crashes in iOS

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

This approach of measuring crashes provides a high-level answer to the question, _Did the user exit my app intentionally?_

Crash reporting libraries provided by companies such as Apteligent \(formerly Crittercism\) use a global `NSException` handler to provide more detailed crash reporting. Your app is not allowed to have more than one of these kinds of handlers. Adobe decided to not implement a global `NSException` handler to prevent build errors, knowing that our customers might be using other crash reporting providers.

## Collecting additional data with Lifecycle

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

