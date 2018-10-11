# Lifecycle API Reference

Lifecycle metrics are valuable, out-of-the-box information about your app user. These metrics contain information on the app user's lifecycle such as device information, install or upgrade information, session start and pause times, etc. You may also choose to set additional, lifecycle metrics. 

{% hint style="warning" %}
This section shows how to start collecting lifecycle metrics. Setup [Analytics](https://aep-sdks.gitbook.io/docs/mobile-extensions/adobe-analytics) or other Experience Cloud solution extensions in order to view, and report on this data in those respective solutions.
{% endhint %}

## Lifecycle start & pause

{% tabs %}
{% tab title="Android" %}
Import the Lifecycle framework:

```java
import com.adobe.marketing.mobile.*;
```

Register the framework with Mobile Core:

```java
public class TargetApp extends Application {
​
 @Override
 public void onCreate() {
     super.onCreate();
     MobileCore.setApplication(this);
​
     try {
         Lifecycle.registerExtension();
     } catch (Exception e) {
         //Log the exception
     }
 }
}
```

With the `onResume` function, start Lifecycle data collection:

```java
@Override  
   public void onResume() {  
      MobileCore.setApplication(getApplication());
      MobileCore.lifecycleStart(null);
   }
```

{% hint style="info" %}
Setting the application is only necessary on activities that are entry points for your application. However, setting the application on each Activity has no negative impact and will ensure that the SDK will always have the necessary reference to your application. So, we recommend calling `setApplication`in each of your activities.
{% endhint %}

Finally, you may use the `onPause` function, to pause the lifecycle data collection:

{% hint style="info" %}
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
#### Objective-C & Swift {#objective-c-and-swift}

Import the Lifecycle framework:

```objectivec
#import <ACPLifecycle_iOS/ACPLifecycle_iOS.h>
#import <ACPCore_iOS/ACPCore_iOS.h>
```

Register the framework with Mobile Core by adding the following in your app's `didFinishLaunchingWithOptions`:

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPLifecycle registerExtension];
​  // Override point for customization after application launch.
  return YES;
}
```

Start Lifecycle data collection by adding `lifecycleStart` to your app's`didFinishLaunchingWithOptions`

```objectivec
// Objective-C
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
  [ACPLifecycle registerExtension];
  [ACPCore lifecycleStart]; 
  return YES; 
}
```

```swift
// Swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
    ACPCore.lifecycleStart(nil)
    return true
}
```

Pause Lifecycle data collection when your app has entered the background:

```objectivec
// Objective-C
 - (void) applicationDidEnterBackground:(UIApplication *)application {
     [ACPCore lifecyclePause];
 }
```

```swift
// Swift
 func applicationDidEnterBackground(_ application: UIApplication) {    
     ACPCore.lifecyclePause()
 }
```
{% endtab %}
{% endtabs %}

## Collect additional data with lifecycle

When you call [Lifecycle start](lifecycle-api-reference.md#lifecycle-start-and-pause) you can, optionally, pass in a dictionary of additional data that will be attached to the lifecycle event.

{% hint style="info" %}
You may pass additional data to lifecycle on app launch, app resume, both, or neither.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
{% hint style="warning" %}

{% endhint %}

```java
@Override
public void onResume() {
    HashMap<String, Object> additionalContextData = new HashMap<String, Object>();
    contextData.put("myapp.category", "Game");
    MobileCore.lifecycleStart(additionalContextData);
}
```

**Java**

{% hint style="warning" %}
You need to add this code only in your main activity and any other activity, from which, your app may be launched.
{% endhint %}
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

```objectivec
// Objective-C
- (void) applicationWillEnterForeground:(UIApplication *)application {      
    [ACPCore lifecycleStart:@{@"state": @"appResume"}];      
}
```

#### Swift

```swift
// Swift
func applicationWillEnterForeground(_ application: UIApplication) {      
    ACPCore.lifecycleStart(["state": "appResume"])
}
```
{% endtab %}
{% endtabs %}

## Tracking App Crashes in 

## Android

If your app is terminated without having first been backgrounded, the SDK an ungraceful close is registered the next time your app is launched. This information helps you understand how closes are tracked and the best practices to handle **false** crashes ****or **ungraceful** closes**.**

{% tabs %}
{% tab title="Android" %}
When lifecycle metrics are implemented, a call is made to `MobileCore.lifecycleStart(additionalContextData)` in the `OnResume` method of each activity. In the `onPause` method, a call is made to `MobileCore.lifecyclePause()`. In the `MobileCore.lifecyclePause()` method, a flag is set to indicate a graceful exit. When the app is launched again or resumed, `MobileCore.lifecycleStart(additionalContextData)` checks this flag. If the app did not exit successfully as determined by the flag status, an `a.CrashEvent` context data is sent with the next call, and a crash event is reported.

{% hint style="info" %}
To ensure accurate crash reporting, you must call `lifecyclePause()` in the `onPause` method of each activity.  For more information about the Android activity lifecycle, see [Activities](https://developer.android.com/guide/components/activities/). 
{% endhint %}

#### **Causes of false crash reporting**

* If you are debugging by using an IDE, such as Android Studio, and launching the app again from the IDE while the app is in the foreground causes a crash.

  **Tip**: You can avoid this crash by backgrounding the app before launching again from the IDE.

* If the previous foreground Activity of your app is moved to the background and does not call `MobileCore.lifecyclePause()`in `onPause`, and your app is manually closed or killed by the operating system, the next launch results in a crash.

#### **Handling fragments**

Fragments have application lifecycle events that are similar to Activities. However, a fragment cannot be active without being attached to an Activity.
{% endtab %}

{% tab title="iOS" %}
This approach of measuring crashes provides a high-level answer to the question, Did the user exit my app intentionally? Crash reporting and app performance vendors use a global `NSException` handler to provide more detailed crash reporting. Your app is not allowed to have more than one of these kinds of handlers. We have decided to not implement a global `NSException` handler to prevent build errors, knowing that our customers might be using other crash reporting providers.

### Cause of false crashes

The following scenarios are known to falsely cause a crash to be reported by the SDK:

* If you are debugging using Xcode, launching the app again while it is in the foreground, causes a crash.

{% hint style="info" %}
You can avoid a crash in this scenario by backgrounding the app before launching the app again from Xcode.
{% endhint %}

* If your app is in the background and sends Analytics hits through a call other than `trackActionFromBackground`, `trackLocation`, or `trackBeacon`, and the app is terminated \(manually or by the operating system\) while in the background, and the next launch will be a crash.

{% hint style="info" %}
Background activity that occurs beyond the `lifecycleTimeout` threshold might also result in an additional false launch.
{% endhint %}

* If your app is launched in the background because of a background fetch, location update, and so on, and is terminated by the operating without coming to the foreground, the next launch \(background or foreground\) results in a crash.
* If you programmatically delete Adobe’s pause flag from `NSUserDefaults`, while the app is in the background, the next launch or resume causes a crash.

### **Preventing false crashes**

The following practices can help prevent false crashes from being reported:

* Ensure that you perform your development against non-production report suites, which should prevent false crash from the first bullet point from occurring.
* Do not delete or modify any values that the Adobe Experience Cloud Platform SDKs puts in `NSUserDefaults`. If these values are modified outside the SDK, the data reported will be invalid.

### **iOS crash reporting**

iOS uses system notifications that allow developers to track and respond to different states and events in the application lifecycle. The Adobe Experience Cloud Platform SDKs has a notification handler that responds to the `UIApplicationDidEnterBackgroundNotification` notification. In this code, a value is set that indicates that the user has backgrounded the app. On a subsequent launch, if that value cannot be found, a crash is reported.
{% endtab %}
{% endtabs %}

## Implementing global lifecycle callbacks {#implementing-global-lifecycle-callbacks}

Starting with API Level 14, Android allows global lifecycle callbacks for activities. For more information, see the [_Android Developers Guide_](https://developer.android.com/reference/android/app/Application#registerActivityLifecycleCallbacks%28android.app.Application.ActivityLifecycleCallbacks).

{% tabs %}
{% tab title="Android" %}
#### Java

You can use these callbacks to ensure that all of your `Activities` correctly call `AdobeMobileMarketing.lifecycleStart()`, and do not need to implement the code for each of the Activity.

```java
import com.adobe.marketing.mobile.*;
​
public class MainActivity extends Activity {
​
    @Override
    protected void onCreate(Bundle savedInstanceState) {     
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
​
        getApplication().registerActivityLifecycleCallbacks(new Application.ActivityLifecycleCallbacks() {
        @Override
        public void onActivityResumed(Activity activity) {
            MobileCore.setApplication(getApplication());
            MobileCore.lifecycleStart(null);
        }
        @Override
        public void onActivityPaused(Activity activity) {
            MobileCore.lifecyclePause();
        }
​
        // the following methods aren't needed for our lifecycle purposes, but are
        // required to be implemented by the ActivityLifecycleCallbacks object
        @Override
        public void onActivityCreated(Activity activity, Bundle savedInstanceState) {}
        @Override
        public void onActivityStarted(Activity activity) {}
        @Override
        public void onActivityStopped(Activity activity) {}
        @Override
        public void onActivitySaveInstanceState(Activity activity, Bundle outState) {}
        @Override
        public void onActivityDestroyed(Activity activity) {}
        });
    }
...
}
```
{% endtab %}
{% endtabs %}



