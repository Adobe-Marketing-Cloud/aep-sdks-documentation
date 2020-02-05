# Initialize the SDK and set up tracking


## Register extensions and starting Core

Besides Mobile Core, all Adobe Experience Platform SDK extensions provide a `registerExtension` API. This API registers the extension with Mobile Core. After an extension is registered, it can dispatch and listen for events. You are required to register each of your extensions before making API calls and failing to do so will lead to undefined behavior.

After you register the extensions you want to use, call the `start` API in Core. This step is required to boot up the SDK for event processing.

The following code snippets demonstrate how to initialize the SDK when using the Identity, Signal, Lifecycle, and Analytics extensions:

{% tabs %}
{% tab title="Android" %}
### Java

```java
try {
    Identity.registerExtension();
    Lifecycle.registerExtension();
    Signal.registerExtension();
    Analytics.registerExtension();
    } catch (Exception e) {
       //Log the exception
    }
}
```
{% endtab %}

{% tab title="iOS" %}
### Objective-C

```objectivec
[ACPIdentity registerExtension];
[ACPLifecycle registerExtension];
[ACPSignal registerExtension];
[ACPAnalytics registerExtension];
[ACPCore start:nil];
```

### Swift

```swift
ACPIdentity.registerExtension()
ACPLifecycle.registerExtension()
ACPSignal.registerExtension()
ACPAnalytics.registerExtension()
ACPCore.start(nil)
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
import {ACPCore, ACPLifecycle, ACPIdentity, ACPSignal, ACPMobileLogLevel} from '@adobe/react-native-acpcore';

initSDK() {
    ACPCore.setLogLevel(ACPMobileLogLevel.VERBOSE);
    ACPCore.configureWithAppId("PASTE_ENVIRONMENT_ID_HERE");
    ACPLifecycle.registerExtension();
    ACPIdentity.registerExtension();
    ACPSignal.registerExtension();
    ACPCore.start();
}
```
{% endtab %}
{% endtabs %}

## Enable lifecycle metrics

{% hint style="warning" %}
This section shows you how to collect lifecycle metrics. To view, and report on this data in those respective solutions, you need to set up [Analytics](../using-mobile-extensions/adobe-analytics/) or other Experience Cloud solution extensions.
{% endhint %}

Lifecycle metrics is an optional, yet valuable feature provided by the Adobe Experience Platform SDK. It provides out-of-the-box, app lifecycle information about your app user. These metrics contain information on the app user's engagement lifecycle such as device information, install or upgrade information, session start and pause times, and so on. You can also set additional lifecycle metrics.

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
#### Objective-C

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

#### Swift

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
### JavaScript

Import the Lifecycle extension

```jsx
import {ACPLifecycle} from '@adobe/react-native-acpcore';
```

Getting the extension version \(optional\)

```jsx
ACPLifecycle.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPLifecycle version: " + version));
```

Registering the extension with Core

```jsx
ACPLifecycle.registerExtension();
```

Starting a lifecycle event

```jsx
ACPCore.lifecycleStart({"lifecycleStart": "myData"});
```

Pausing a lifecycle event

```jsx
ACPCore.lifecyclePause();
```
{% endtab %}
{% endtabs %}

For more information, see [Lifecycle Metrics](../using-mobile-extensions/mobile-core/lifecycle/).

## Track screens and user actions

You can use the following screen and action tracking APIs to measure your user's engagement with your app.

Actions are events that occur in your app. Use this API to track and measure an action, where each action has one or more corresponding metrics that increment each time the event occurs. For example, you might call this API for each new subscription each time an article is viewed, or each time a level is completed.

{% hint style="warning" %}
This section shows you how to start tracking app screens and user actions. To view and report on this data in those respective solutions, set up [Analytics](../using-mobile-extensions/adobe-analytics/) or other Experience Cloud solution extensions.
{% endhint %}

### Track user actions

{% hint style="warning" %}
You must call this API when an event that you want to track occurs. In addition to the action name, you can send additional context data with each track action call.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java <a id="java"></a>

### trackAction <a id="trackaction"></a>

#### Syntax <a id="syntax"></a>

```java
public static void trackAction(final String action, final Map<String, String> contextData)
```

#### Example <a id="example"></a>

```java
Map<String, String> additionalContextData = new HashMap<String, String>();
additionalContextData.put("customKey", "value");
MobileCore.trackAction("loginClicked", additionalContextData);
```
{% endtab %}

{% tab title="iOS" %}
### trackAction

### Objective-C

#### Syntax

```csharp
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

#### Example

```c
 [ACPCore trackAction:@"action name" data:@{@"key":@"value"}];
```

### Swift

#### Syntax

```c
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

#### Example

```c
ACPCore.trackAction("action name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
ACPCore.trackAction("action", {"mytest": "action"});
```
{% endtab %}
{% endtabs %}

### Track app states and screens

States represent screens or views in your app. Each time a new state is displayed in your application, for example, when a user navigates from the home page to the news feed, this method might be called. This method also sends an Analytics state tracking hit with optional context data.

{% tabs %}
{% tab title="Android" %}
#### Java

In Android, `trackState` is typically called each time a new activity is loaded.

### trackState <a id="trackstate"></a>

#### **Syntax** <a id="syntax-1"></a>

```java
public static void trackState(final String state, final Map<String, String> contextData)
```

#### Example <a id="example-1"></a>

```java
Map<String, String> additionalContextData = new HashMap<String, String>();         
additionalContextData.put("customKey", "value");         
MobileCore.trackState("homePage", additionalContextData);
```
{% endtab %}

{% tab title="iOS" %}
### trackState

### Objective-C

#### Syntax

```c
 + (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

#### Example

```c
 [ACPCore trackState:@"state name" data:@{@"key":@"value"}];
```

### Swift

#### Syntax

```c
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

#### Example

```c
ACPCore.trackState("state name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
ACPCore.trackState("state", {"mytest": "state"});
```
{% endtab %}
{% endtabs %}

For more information, see [Mobile Core API Reference](../using-mobile-extensions/mobile-core/mobile-core-api-reference.md).

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://helpx.adobe.com/contact/enterprise-support.ec.html) for immediate assistance

