# Initialize the SDK and Set up Tracking

## Configure SDK with the Launch Environment ID

To initialize the SDK, you'll first need to configure the SDK with the Environment ID from Launch.

{% hint style="info" %}
To find your Environment ID, navigate to Environments tab in Launch, and click on the ![](../.gitbook/assets/screen-shot-2018-10-18-at-11.22.17-am.png)icon corresponding to the environment you are setting up.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
{% hint style="warning" %}
_Adobe Experience Platform SDK for Android supports **Android 4.0 \(API 14\) or later.**_
{% endhint %}

1. Create MainActivity.java in the app.
2. Add `MobileCore.configureWithAppID("PASTE_ENVIRONMENT_ID_HERE");`
{% endtab %}

{% tab title="Objective C" %}
{% hint style="warning" %}
Adobe Experience Platform SDK for iOS supports **iOS 10 or later.**
{% endhint %}

1. In Xcode, open AppDelegate.swift
2. Under `didFinishLaunchingWithOptions`, add:`[ACPCore configureWithAppId:@"PASTE_ENVIRONMENT_ID_HERE"];`
{% endtab %}

{% tab title="Swift" %}
{% hint style="warning" %}
Adobe Experience Platform SDKs for iOS supports **iOS 10 or later.**
{% endhint %}

1. In Xcode, open AppDelegate.swift
2. Under `didFinishLaunchingWithOptions`, add:`ADBMobileMarketing.configure(withAppId: "PASTE_ENVIRONMENT_ID_HERE")`
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Developing extensions and using Launch Integration? The environment ID should be prefixed with `staging/`. For example, `staging/launch-EN58bc2c40c3b14d688b768fe79a623519-development`
{% endhint %}

## Enable debug logging

Debug logging is optional and helps you ensure that the SDK is working as intended. Below is a table that explains the levels of logging available and when they may be used:

| Log Level | Description |
| :--- | :--- |
| Error | This log level details unrecoverable errors caused during SDK implementation. |
| Warning | In addition to detail from **Error** log level, **Warning** provides error information during SDK integration. This log level may indicate that a request has been made to the SDK, but the SDK may be unable to perform the requested task. For example, this may be used when catching an unexpected but recoverable exception and printing its message. |
| Debug | In addition to detail from **Warning** log level, **Debug** also provides high-level information on how the SDK processes network requests/responses data. |
| Verbose | In addition to detail from the **Debug** level, **Verbose** provides detailed, low-level information into how SDK processes database interactions and SDK events.  |

To enable debug logging:

{% tabs %}
{% tab title="Android" %}
```java
MobileCore.setLogLevel(LoggingMode.DEBUG);
// MobileCore.setLogLevel(LoggingMode.VERBOSE);
// MobileCore.setLogLevel(LoggingMode.WARNING);
// MobileCore.setLogLevel(LoggingMode.ERROR);
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
[ACPCore setLogLevel:ACPMobileLogLevelDebug];
// [ACPCore setLogLevel:ACPMobileLogLevelVerbose];
// [ACPCore setLogLevel:ACPMobileLogLevelWarning];
// [ACPCore setLogLevel:ACPMobileLogLevelError];
```
{% endtab %}

{% tab title="Swift" %}
```swift
ACPCore.setLogLevel(ACPMobileLogLevel.debug)
// ACPCore.setLogLevel(ACPMobileLogLevel.verbose)
// ACPCore.setLogLevel(ACPMobileLogLevel.warning)
// ACPCore.setLogLevel(ACPMobileLogLevel.error)
```
{% endtab %}
{% endtabs %}

## Enable the Experience Cloud Identity service

The Experience Cloud ID service provides a universal visitor ID across Experience Cloud solutions and is pre-requisite for most implementations. 

{% hint style="info" %}
Ensure that you have the right Experience Cloud Org ID in the Mobile Core settings page, as mentioned in [Get the SDK](get-the-sdk.md).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
Import the Identity framework into your project:

`import com.adobe.marketing.mobile.*;`

Register the framework with Mobile Core:

```java
public class MobiletApp extends Application {
  @Override
  public void onCreate(){
     super.onCreate();
     MobileCore.setApplication(this);
     try {
        Identity.registerExtension();
     } catch (Exception e) {
       //Log the exception
       }
    }
 }
```
{% endtab %}

{% tab title="Objective-C" %}
Add the Identity framework \(contained within **Core**\) into your project

```text
#import <ACPIdentity_iOS/ACPIdentity_iOS.h>
```

Register the Identity framework with the **Core**

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```
{% endtab %}

{% tab title="Swift" %}
Add the Identity framework \(contained within **Core**\) into your bridging header

```text
#import <ACPIdentity_iOS/ACPIdentity_iOS.h>
```

Register the Identity framework with the **Core**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
  ACPIdentity.registerExtension()
  return true
}
```
{% endtab %}
{% endtabs %}

After successful configuration, you'll see the Experience Cloud ID generated and included on every network hit sent to Adobe. Other automatically generated and custom will also be sent with each hit.

## Enable lifecycle metrics

{% hint style="warning" %}
This section shows how to start collecting lifecycle metrics. Setup [Analytics](../using-mobile-extensions/adobe-analytics/) or other Experience Cloud solution extensions in order to view, and report on this data in those respective solutions.
{% endhint %}

Lifecycle metrics are valuable, out-of-the-box information about your app user.  These metrics contain information on the app user's lifecycle such as device information, install or upgrade information, session start and pause times, etc. You may also choose to set additional, lifecycle metrics.

{% tabs %}
{% tab title="Android" %}
#### Java

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
#### Objective-C & Swift

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

See [Lifecycle Metrics](../using-mobile-extensions/mobile-core/lifecycle/), for complete usage reference.

## Track screens and user actions

You may use the following screen and action tracking APIs in order to start measuring your user's engagement with your app.

Actions are events that occur in your app. Use this API to track and measure an action - each action has one or more corresponding metrics that are incremented each time the event occurs. For example, you might call this API for each new subscription each time an article is viewed, or each time a level is completed.

{% hint style="warning" %}
This section shows how to start tracking app screens and user actions. Setup [Analytics](../using-mobile-extensions/adobe-analytics/) or other Experience Cloud solution extensions in order to view, and report on this data in those respective solutions.
{% endhint %}

### Track user actions

{% hint style="warning" %}
You must call this API when an event that you want to track, occurs. In addition to the action name, you may send additional context data with each track action call. 
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java {#java}

### trackAction {#trackaction}

#### Syntax {#syntax}

```java
public static void trackAction(final String action, final Map<String, String> contextData)
```

#### Example {#example}

```java
Map<String, String> additionalContextData = new HashMap<String, String>();
additionalContextData.put("customKey", "value");
MobileCore.trackAction("loginClicked", additionalContextData);
```
{% endtab %}

{% tab title="Objective-C" %}
### trackAction

#### Syntax

```csharp
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

#### Example

```c
 [ACPCore trackAction:@"action name" data:@{@"key":@"value"}];
```
{% endtab %}

{% tab title="Swift" %}
### trackAction

#### Syntax

```c
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

#### Example

```c
ACPCore.trackAction("action name", data: ["key": "value"])
```
{% endtab %}
{% endtabs %}

### Track app states and screens

States represent screens or views in your app. Each time a new state is displayed in your application, for example, when a user navigates from the home page to the news feed, this API may be called.. This method sends an Analytics state tracking hit with optional context data.

{% tabs %}
{% tab title="Android" %}
#### Java

 In Android, trackState is typically called each time a new activity is loaded

### trackState {#trackstate}

#### **Syntax** {#syntax-1}

```java
public static void trackState(final String state, final Map<String, String> contextData)
```

#### Example {#example-1}

```java
Map<String, String> additionalContextData = new HashMap<String, String>();         
additionalContextData.put("customKey", "value");         
MobileCore.trackState("homePage", additionalContextData);
```
{% endtab %}

{% tab title="Objective-C" %}
### trackState

#### Syntax

```c
 + (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

#### Example

```c
 [ACPCore trackState:@"state name" data:@{@"key":@"value"}];
```
{% endtab %}

{% tab title="Swift" %}
### trackState

#### Syntax

```c
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

#### Example

```c
ACPCore.trackState("state name", data: ["key": "value"])
```
{% endtab %}
{% endtabs %}

See [Mobile Core API Reference](../using-mobile-extensions/mobile-core/configuration-reference/mobile-core-api-reference.md), for complete usage reference.

