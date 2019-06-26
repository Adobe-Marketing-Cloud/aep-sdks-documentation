# Initialize the SDK and set up tracking

## Configure SDK with the Experience Platform Launch Environment ID

To initialize the SDK, you need to first configure the SDK with an Environment ID from Experience Platform Launch.

{% hint style="info" %}
To find your Environment ID, in Experience Platform Launch, go to the **Environments** tab and click on the ![](../.gitbook/assets/screen-shot-2018-10-18-at-11.22.17-am.png)icon that corresponds to the environment that you are setting up.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
{% hint style="warning" %}
Adobe Experience Platform SDK for Android supports Android 4.0 \(API 14\) or later.
{% endhint %}

#### Ensure app permissions

The SDK requires standard [network connection](https://developer.android.com/training/basics/network-ops/connecting) permissions in your manifest to send data, collect cellular provider, and record offline tracking calls.

To add these permissions, add the following lines to your `AndroidManifest.xml` file, which is located in the application project directory:

```markup
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

#### Java

1. In the app, create `MainActivity.java` .
2. Add `MobileCore.configureWithAppID("PASTE_ENVIRONMENT_ID_HERE");`
{% endtab %}

{% tab title="Objective-C" %}
{% hint style="warning" %}
Adobe Experience Platform SDK for iOS supports **iOS 10 or later.**
{% endhint %}

#### Objective-C

In Xcode, find your `didFinishLaunchingWithOptions` in `AppDelegate.h` and add:

```objectivec
[ACPCore configureWithAppId:@"PASTE_ENVIRONMENT_ID_HERE"];
```
{% endtab %}

{% tab title="Swift" %}
{% hint style="warning" %}
Adobe Experience Platform SDK for iOS supports **iOS 10 or later.**
{% endhint %}

#### Swift

In Xcode, find your `didFinishLaunchingWithOptions` in AppDelegate.swift and add:

```swift
ACPCore.configure(withAppId: "PASTE_ENVIRONMENT_ID_HERE")
```
{% endtab %}

{% tab title="React Native" %}
### **Initializing the SDK**

It is recommended to initialize the SDK in your native code inside your AppDelegate and MainApplication in iOS and Android respectively, however you can still initialize the SDK in Javascript.

**iOS**

```jsx
// Import the SDK
#import <RCTACPCore/ACPCore.h>
#import <RCTACPCore/ACPLifecycle.h>
#import <RCTACPCore/ACPIdentity.h>
#import <RCTACPCore/ACPSignal.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  //...
  [ACPCore configureWithAppId:@"PASTE_ENVIRONMENT_ID_HERE"];
  [ACPCore setWrapperType:ACPMobileWrapperTypeReactNative];
  [ACPIdentity registerExtension];
  [ACPLifecycle registerExtension];
  [ACPSignal registerExtension];
  
  [ACPCore start:nil];
}
```

**Android**

```jsx
@Override
public void onCreate() {
  //...
  MobileCore.setApplication(this);
  MobileCore.configureWithAppID("PASTE_ENVIRONMENT_ID_HERE");
  MobileCore.setWrapperType(WrapperType.REACT_NATIVE);
  try {
    Identity.registerExtension();
    Lifecycle.registerExtension();
    Signal.registerExtension();
  } catch (Exception e) {
    // handle exception
  }

  MobileCore.start(null);
}
```

**Javascript**

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

{% hint style="info" %}
Developing extensions and using an Experience PlatformLaunch Integration? The environment ID should be prefixed with `staging/`. For example, `staging/launch-EN58bc2c40c3b14d688b768fe79a623519-development`
{% endhint %}

## Enable debug logging

Debug logging is optional and helps you ensure that the SDK is working as intended. Below is a table that explains the levels of logging available and when they may be used:

| Log Level | Description |
| :--- | :--- |
| Error | This log level provides the details about unrecoverable errors that occurred during SDK implementation. |
| Warning | In addition to the detail from _Error_ log level, _Warning_ provides error information during SDK integration. This log level might indicate that a request has been made to the SDK, but the SDK might be unable to perform the requested task. For example, this log level might be used when catching an unexpected, but recoverable, exception and printing its message. |
| Debug | In addition to detail from the _Warning_ log level, _Debug_ also provides high-level information about how the SDK processes network requests/responses data. |
| Verbose | In addition to detail from the _Debug_ level, _Verbose_ provides detailed, low-level information about how SDK processes database interactions and SDK events. |

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

{% tab title="React Native" %}
Enable and control the log level of the SDK

```jsx
import {ACPMobileLogLevel} from '@adobe/react-native-acpcore';

ACPCore.setLogLevel(ACPMobileLogLevel.VERBOSE);
```

```jsx
const ERROR = "ACP_LOG_LEVEL_ERROR";
const WARNING = "ACP_LOG_LEVEL_WARNING";
const DEBUG = "ACP_LOG_LEVEL_DEBUG";
const VERBOSE = "ACP_LOG_LEVEL_VERBOSE";
```
{% endtab %}
{% endtabs %}

## Registering Extensions and Starting Core

Other than the Mobile Core extension, all Experience Platform extensions provide a `registerExtension` API, which registers the extension with Core. After you register the extension, you can dispatch and listen for events. You are required to register each of your extensions before making API calls and failing to do so will lead to undefined behavior.

After you register all of your extensions, call the `start` API in Core. This step is required to boot up the SDK for event processing.

The following code snippets demonstrate how to initialize the SDK when using the Identity, Signal, Lifecycle, and Analytics extensions:

{% tabs %}
{% tab title="Android" %}
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

{% tab title="Objective-C" %}
```objectivec
[ACPIdentity registerExtension];
[ACPLifecycle registerExtension];
[ACPSignal registerExtension];
[ACPAnalytics registerExtension];
[ACPCore start:nil];
```
{% endtab %}

{% tab title="Swift" %}
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

## Enable the Experience Cloud Identity service

Formerly known as Marketing Cloud ID \(MCID\), the Experience Cloud ID \(ECID\) service provides a cross-channel notion of identity across Experience Cloud solutions and is a prerequisite for most implementations.

{% hint style="info" %}
To confirm that you have the correct Experience Cloud Org ID in the Mobile Core settings page, see [Get the SDK](get-the-sdk.md).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
Import the Identity framework to your project:

#### Java

```java
import com.adobe.marketing.mobile.*;
```

Register the framework with Mobile Core:

```java
public class MobileApp extends Application {
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

{% tab title="iOS" %}
Add the Identity framework to your project:

#### Objective-C

```objectivec
#import "ACPIdentity.h"
```

#### Swift

```swift
import ACPCore
```

Register the Identity framework with Mobile Core

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
  ACPIdentity.registerExtension()
  return true
}
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

Import the Identity extension

```jsx
import {ACPIdentity} from '@adobe/react-native-acpcore';
```

Get the extension version \(optional\)

```jsx
ACPIdentity.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPIdentity version: " + version));
```

Register the extension with Core

```jsx
ACPIdentity.registerExtension();
```
{% endtab %}
{% endtabs %}

After a successful configuration, the Experience Cloud ID is generated and included on every network hit that is sent to Adobe. Other automatically generated and custom are also sent with each hit.

## Enable lifecycle metrics

{% hint style="warning" %}
This section shows you how to collect lifecycle metrics. To view, and report on this data in those respective solutions, you need to set up [Analytics](../using-mobile-extensions/adobe-analytics/) or other Experience Cloud solution extensions.
{% endhint %}

Lifecycle metrics contain valuable, out-of-the-box information about your app user. These metrics contain information on the app user's lifecycle such as device information, install or upgrade information, session start and pause times, and so on. You can also set additional lifecycle metrics.

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
#import  "ACPLifecycle.h"
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
  [ACPCore start:^{
        [ACPCore lifecycleStart:nil];
    }];
  return YES; 
}
```

Pause Lifecycle data collection when your app has entered the background:

```objectivec
 // Objective-C
 - (void) applicationDidEnterBackground:(UIApplication *)application {
     [ACPCore lifecyclePause];
 }
```

#### Swift

In swift, ACPCore includes ACPLifecycle :

```swift
import ACPCore
```

Register the framework with Mobile Core by adding the following in your app's `didFinishLaunchingWithOptions`:

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
ACPLifecycle.registerExtension();
​  // Override point for customization after application launch.
  return true;
}
```

Start Lifecycle data collection by adding `lifecycleStart` to your app's`didFinishLaunchingWithOptions`

```swift
// Swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
ACPCore.start {
    ACPCore.lifecycleStart(nil);
}
    return true
}
```

Pause Lifecycle data collection when your app has entered the background:

```swift
// Swift
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
#### Java   <a id="java"></a>

### trackAction   <a id="trackaction"></a>

#### Syntax   <a id="syntax"></a>

```java
public static void trackAction(final String action, final Map<String, String> contextData)
```

#### Example   <a id="example"></a>

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

### trackState   <a id="trackstate"></a>

#### **Syntax**   <a id="syntax-1"></a>

```java
public static void trackState(final String state, final Map<String, String> contextData)
```

#### Example   <a id="example-1"></a>

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

{% tab title="React Native" %}
### JavaScript

```jsx
ACPCore.trackState("state", {"mytest": "state"});
```
{% endtab %}
{% endtabs %}

For more information, see [Mobile Core API Reference](../using-mobile-extensions/mobile-core/mobile-core-api-reference.md).

