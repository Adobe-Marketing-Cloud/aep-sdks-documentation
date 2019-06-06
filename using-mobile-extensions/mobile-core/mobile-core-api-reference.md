# Mobile Core API reference

## Application reference

When building Android applications, the `android.app.Application` reference must be passed to the Mobile SDK, which allows the Mobile SDK to access the `android.app.Context` and monitor the lifecycle of the Android application.

{% hint style="warning" %}
Android applications must call `MobileCore.setApplication()` before calling any other Mobile SDK API.
{% endhint %}

The following APIs are also required in your mobile app:

```java
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
   ACPCampaign.registerExtension();
   ACPIdentity.registerExtension();
   ACPLifecycle.registerExtension();
   ACPSignal.registerExtension();   
   ACPUserProfile.registerExtension();
   ACPCore.start();
  // Override point for customization after application launch.
  return true;
}
```

{% tabs %}
{% tab title="Android" %}
**Java**

#### setApplication

**Syntax**

```java
public static void setApplication(final Application app)
```

**Example**

```java
public class CoreApp extends Application {

   @Override
   public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);
      MobileCore.start(null);
   }
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Android" %}
**Java**

#### getApplication

{% hint style="warning" %}
`MobileCore.getApplication` might return `null` if the Application object was destroyed or if `MobileCore.setApplication` was not previously called.
{% endhint %}

**Syntax**

```java
public static Application getApplication()
```

**Example**

```java
Application app = MobileCore.getApplication();
if (app != null) {
    ...
}
```
{% endtab %}
{% endtabs %}

### Track app actions

Actions are events that occur in your app. You can use this API to track and measure an action. Each action has one or more corresponding metrics that are incremented each time the event occurs. For example, you might call this API for each new subscription each time an article is viewed, or each time a level is completed.

{% hint style="warning" %}
Call this API when an event that you want to track occurs. In addition to the action name, you can send additional context data with each track action call.
{% endhint %}

{% hint style="info" %}
If you have the **Analytics** extension set up, this method sends an Analytics action tracking hit with the optional context data that you provide.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

#### trackAction

**Syntax**

```java
public static void trackAction(final String action, final Map<String, String> contextData)
```

**Example**

```java
Map<String, String> additionalContextData = new HashMap<String, String>();
additionalContextData.put("customKey", "value");
MobileCore.trackAction("loginClicked", additionalContextData);
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

#### trackAction

**Syntax**

```objectivec
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

**Example**

```objectivec
 [ACPCore trackAction:@"action name" data:@{@"key":@"value"}];
```

**Swift**

#### trackAction

**Syntax**

```swift
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

**Example**

```swift
ACPCore.trackAction("action name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

#### trackAction

```jsx
ACPCore.trackAction("action-name", {"key": "value"});
```
{% endtab %}
{% endtabs %}

### Track app states and views

States represent screens or views in your app. Each time a new state is displayed in your application, for example, when a user navigates from the home page to the news feed, this API can be called. This method sends an Analytics state tracking hit with optional context data.

{% hint style="info" %}
If you have the Analytics extension set up, this API increments page views and an Analytics state tracking hit with the optional context data that you provide.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

In Android, `trackState` is typically called each time a new Activity is loaded.

#### trackState     <a id="trackstate"></a>

**Syntax**

```text
public static void trackState(final String state, final Map<String, String> contextData)
```

**Example**

```text
Map<String, String> additionalContextData = new HashMap<String, String>();         additionalContextData.put("customKey", "value");         MobileCore.trackState("homePage", additionalContextData);
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

#### trackState

**Syntax**

```objectivec
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

**Example**

```objectivec
 [ACPCore trackState:@"state name" data:@{@"key":@"value"}];
```

**Swift**

#### trackState

**Syntax**

```objectivec
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

**Example**

```swift
ACPCore.trackState("state name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

#### trackState

```jsx
ACPCore.trackState("state-name", {"key": "value"});
```
{% endtab %}
{% endtabs %}

### Collect PII

This API allows the SDK to collect sensitive or personally identifiable information \(PII\) data.

{% hint style="warning" %}
While this API enables the collection of sensitive data, no data is actually sent to any Adobe or third-party endpoints. To send the data to an endpoint, use a postback of the PII type.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

#### collectPii

**Syntax**

```java
public static void collectPII(final Map<String, String> piiData);
```

**Example**

```java
Map<String, String> data = new HashMap<String, String>();
data.put("firstname", "customer");
//The rule to trigger a PII needs to be setup for this call
//to result in a network send
MobileCore.collectPII(data);
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

#### collectPii

**Syntax**

```objectivec
+ (void) collectPii: (nonnull NSDictionary<NSString*, NSString*>*) data;
```

**Example**

```objectivec
[ACPCore collectPii:data:@{@"key1" : "@value1",
                           @"key2" : "@value2"
                           }];
```

**Swift**

#### collectPii

**Syntax**

```swift
ACPCore.collectPii(data: [String : String])
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
ACPCore.collectPii({"myPii": "data"});
```
{% endtab %}
{% endtabs %}

### Collect launch information

You can provide the user information to the SDK from various launch points in your application.

{% hint style="info" %}
If the Analytics extension is enabled in your SDK, collecting this launch data results in an Analytics request being sent. Other extensions in the SDK might use the collected data, for example, as a rule condition for an In-App Message.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
Coming soon
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

This method should be called to support the following use cases:

* Tracking Deep Link click-throughs
  * From `application:didFinishLaunchingWithOptions`
  * Extract `userInfo` from `UIApplicationLaunchOptionsURLKey`
* Tracking Push Message click-through
  * From `application:didReceiveRemoteNotification:fetchCompletionHandler:`

#### collectLaunchInfo

**Syntax**

```text
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

**Example**

```text
 [ACPCore collectLaunchInfo:launchOptions];
```

**Swift**

This method should be called to support the following use cases:

* Tracking Deep Link click-throughs
  * From `application(_:didFinishLaunchingWithOptions:)`
  * Extract `userInfo` from `url: UIApplication.LaunchOptionsKey`
* Tracking Push Message click-through
  * From `application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`

#### collectLaunchInfo

**Syntax**

```swift
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

**Example**

```swift
ACPCore.collectLaunchInfo(userInfo)
```
{% endtab %}
{% endtabs %}

### Logging

The logging APIs allow log messages to be tagged and filtered with the Mobile SDK log messages and allow the application developer to filter the logged messages based on current logging mode.

Application developers can use the `setLogLevel` API to filter the log messages that are coming from the Mobile SDK. When debugging, use `LoggingMode.VERBOSE` \(Android\) / `ACPMobileLogLevelVerbose` \(iOS\) to enable all the logging messages coming from the Mobile SDK and partner extensions. In a production application, we recommend that you use a less verbose logging mode, for example `LoggingMode.ERROR` \(Android\) / `ACPMobileLogLevelError` \(iOS\).

By default, the Mobile SDK logging mode is set to `LoggingMode.ERROR` \(Android\) / `ACPMobileLogLevelError` \(iOS\).

As a Mobile SDK extension developer, use the MobileCore \(Android\) / ACPCore \(iOS\) `log` API to include extension log messages with Mobile SDK core log messages.

From least to most verbose, the order of the mobile SDK logging modes is as follows:

* ERROR
* WARNING
* DEBUG
* VERBOSE

{% hint style="info" %}
In Android, Mobile SDK uses `android.util.Log` class for printing the messages.

In iOS, Mobile SDK uses `NSLog` for logging the message to Apple System Log facility.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

#### setLogLevel

**Syntax**

```java
public static void setLogLevel(LoggingMode mode)
```

**Example**

```java
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
...

MobileCore.setLogLevel(LoggingMode.VERBOSE);
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

#### setLogLevel

**Syntax**

```text
+ (void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```text
#import "ACPCore.h"
...

[ACPCore setLogLevel: ACPMobileLogLevelVerbose];
```

**Swift**

#### setLogLevel

**Syntax**

```swift
+ (void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```swift
import ACPCore
...

ACPCore.setLogLevel(ACPMobileLogLevel.verbose);
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

#### setLogLevel

```jsx
import {ACPMobileLogLevel} from '@adobe/react-native-acpcore';

ACPCore.setLogLevel(ACPMobileLogLevel.VERBOSE);
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Android" %}
**Java**

#### getLogLevel

**Syntax**

```java
public static LoggingMode getLogLevel()
```

**Example**

```java
LoggingMode mode = MobileCore.getLogLevel();
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

#### getLogLevel

**Syntax**

```text
+ (ACPMobileLogLevel) logLevel;
```

**Example**

```text
var logLevel:ACPMobileLogLevel = [ACPCore logLevel];
```

**Swift**

#### getLogLevel

**Syntax**

```swift
+ (ACPMobileLogLevel) logLevel;
```

**Example**

```swift
let logLevel:ACPMobileLogLevel = ACPCore.logLevel();
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

#### getLogLevel

```jsx
ACPCore.getLogLevel().then(level => console.log("AdobeExperienceSDK: Log Level = " + level));
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Android" %}
**Java**

The `MobileCore` logging APIs use the `android.util.Log` APIs to log messages to Android. Based on the `LoggingMode` passed to `MobileCore.log()`, the following Android method is called:

* `LoggingMode.VERBOSE` uses `android.util.Log.v`
* `LoggingMode.DEBUG` uses `android.util.Log.d`
* `LoggingMode.WARNING` uses `android.util.Log.w`
* `LoggingMode.ERROR` uses `android.util.Log.e`

All log messages from the Adobe Experience SDK to Android use the same log tag of `AdobeExperienceSDK`. For example, if logging an error message is using `MobileCore.log()`, the call to `android.util.Log.e` looks like `Log.e("AdobeExperienceSDK", tag + " - " + message)`.

#### log

**Syntax**

```java
public static void log(final LoggingMode mode, final String tag, final String message)
```

**Example**

```java
MobileCore.log(LoggingMode.DEBUG, "MyClassName", "Provided data was null");
```

**Output Example**

```text
D/AdobeExperienceSDK: MyClassName - Provided data was null
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

The log messages from the Adobe Experience SDK are printed to the Apple System Log facility and use a common format that contains the tag `AdobeExperienceSDK`. For example, if logging an error message using `ACPCore.log()`, the printed output looks like `[AdobeExperienceSDK ERROR <tag>]: message`.

#### log

**Syntax**

```text
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

**Example**

```text
[ACPCore log: ACPMobileLogLevelDebug, tag:@"MyClassName", message:@"Provided data was nil"];
```

**Output Example**

```text
[AdobeExperienceSDK DEBUG <MyClassName>]: Provided data was nil
```

**Swift**

#### log

**Syntax**

```swift
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

**Example**

```swift
ACPCore.log(ACPMobileLogLevel.debug, tag: "MyClassName", message: "Provided data was nil");
```

**Output Example**

```text
[AdobeExperienceSDK DEBUG <MyClassName>]: Provided data was nil
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

The log messages from the Adobe Experience SDK are printed to the Log facility and use a common format that contains the tag `ACPMobileLogLevel`. For example, if logging an error message using `ACPCore.log()`, the printed output looks like 

```jsx
ACPCore.log(ACPMobileLogLevel.ERROR, "React Native Tag", "React Native Message");
```

Note: `ACPMobileLogLevel` contains the following getters:

```jsx
const ERROR = "ACP_LOG_LEVEL_ERROR";
const WARNING = "ACP_LOG_LEVEL_WARNING";
const DEBUG = "ACP_LOG_LEVEL_DEBUG";
const VERBOSE = "ACP_LOG_LEVEL_VERBOSE";
```
{% endtab %}
{% endtabs %}

### Additional Information

* What is [context data](https://marketing.adobe.com/resources/help/en_US/sc/implement/context_data_variables.html)?

