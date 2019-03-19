# Mobile Core API reference

## Track app actions

Actions are events that occur in your app. Use this API to track and measure an action. Each action has one or more corresponding metrics that are incremented each time the event occurs. For example, you might call this API for each new subscription each time an article is viewed, or each time a level is completed.

{% hint style="warning" %}
Call this API when an event that you want to track occurs. In addition to the action name, you can send additional context data with each track action call.
{% endhint %}

{% hint style="info" %}
If you have the **Analytics** extension set up, this method sends an Analytics action tracking hit with the optional context data that you provide.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

### trackAction

#### Syntax

```java
public static void trackAction(final String action, final Map<String, String> contextData)
```

#### Example

```java
Map<String, String> additionalContextData = new HashMap<String, String>();
additionalContextData.put("customKey", "value");
MobileCore.trackAction("loginClicked", additionalContextData);
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

### trackAction

#### Syntax

```objectivec
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

#### Example

```objectivec
 [ACPCore trackAction:@"action name" data:@{@"key":@"value"}];
```

#### Swift

### trackAction

#### Syntax

```swift
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

#### Example

```swift
ACPCore.trackAction("action name", data: ["key": "value"])
```
{% endtab %}
{% endtabs %}

## Track app states and views

States represent screens or views in your app. Each time a new state is displayed in your application, for example, when a user navigates from the home page to the news feed, this API can be called. This method sends an Analytics state tracking hit with optional context data.

{% hint style="info" %}
If you have the **Analytics** extension set up, this API increments page views and an Analytics state tracking hit with the optional context data that you provide.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

In Android, `trackState` is typically called each time a new Activity is loaded.

### trackState  <a id="trackstate"></a>

#### **Syntax**  <a id="syntax-1"></a>

```text
public static void trackState(final String state, final Map<String, String> contextData)
```

#### Example  <a id="example-1"></a>

```text
Map<String, String> additionalContextData = new HashMap<String, String>();         additionalContextData.put("customKey", "value");         MobileCore.trackState("homePage", additionalContextData);
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

### trackState

#### Syntax

```objectivec
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

#### Example

```objectivec
 [ACPCore trackState:@"state name" data:@{@"key":@"value"}];
```

#### Swift

### trackState

#### Syntax

```objectivec
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

#### Example

```swift
ACPCore.trackState("state name", data: ["key": "value"])
```
{% endtab %}
{% endtabs %}

## Collect PII

This API allows the SDK to collect sensitive or personally identifiable information \(PII\) data.

{% hint style="warning" %}
While this API enables the collection of sensitive data, no data is actually sent to any Adobe or third-party endpoints. To send the data to an endpoint, use a postback of the PII type.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

### collectPii

#### Syntax

```java
public static void collectPII(final Map<String, String> piiData);
```

#### Example

```java
Map<String, String> data = new HashMap<String, String>();
data.put("firstname", "customer");
//The rule to trigger a PII needs to be setup for this call
//to result in a network send
MobileCore.collectPII(data);
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

### collectPii

#### Syntax

```objectivec
+ (void) collectPii: (nonnull NSDictionary<NSString*, NSString*>*) data;
```

#### Example

```objectivec
[ACPCore collectPii:data:@{@"key1" : "@value1",
                           @"key2" : "@value2"
                           }];
```

#### Swift

### collectPii

#### Syntax

```swift
ACPCore.collectPii(data: [String : String])
```
{% endtab %}
{% endtabs %}

## Collect launch information

You can provide the user information to the SDK from various launch points in your application.

{% hint style="info" %}
If the **Analytics** extension is enabled in your SDK, collecting this launch data results in an Analytics request being sent. Other extensions in the SDK might use the collected data, for example, as a rule condition for an In-App Message.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
Coming soon
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

This method should be called to support the following use cases:

* Tracking Deep Link click-throughs
  * From `application:didFinishLaunchingWithOptions`
  * Extract `userInfo` from `UIApplicationLaunchOptionsURLKey`
* Tracking Push Message click-through
  * From `application:didReceiveRemoteNotification:fetchCompletionHandler:`

### collectLaunchInfo

#### Syntax

```text
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

#### Example

```text
 [ACPCore collectLaunchInfo:launchOptions];
```

#### Swift

This method should be called to support the following use cases:

* Tracking Deep Link click-throughs
  * From `application(_:didFinishLaunchingWithOptions:)`
  * Extract `userInfo` from `url: UIApplication.LaunchOptionsKey`
* Tracking Push Message click-through
  * From `application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`

### collectLaunchInfo

#### Syntax

```swift
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

#### Example

```swift
ACPCore.collectLaunchInfo(userInfo)
```
{% endtab %}
{% endtabs %}

## Logging

The logging APIs allow log messages to be tagged and filtered with the Mobile SDK log messages. It allows a separation between Mobile SDK messages and application messages in the device log files. 

As an application developer, use the `setLogLevel` API to filter the log messages coming from the Mobile SDK.

As a Mobile SDK extension developer, use the `log` APIs to include extension log messages with Mobile SDK core log messages.

The Mobile SDK logging modes in order of verbosity, from least to most, are `ERROR`, `WARNING`, `DEBUG`, and `TRACE`.



{% tabs %}

{% tab title="Android" %}

#### Java

### setLogLevel

#### Syntax

```java
public static void setLogLevel(LoggingMode mode)
```

#### Example

```java
MobileCore.setLogLevel(com.adobe.marketing.mobile.LoggingMode.VERBOSE);
```

{% endtab %}

{% tab title="Objective-C" %}

#### Objective-C

### setLogLevel

#### Syntax

```objective-c
+ (void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

#### Example

```objective-c
[ACPCore setLogLevel: ACPMobileLogLevelVerbose];
```

{% endtab %}

{% tab title="Swift" %}

#### Swift

### setLogLevel

#### Syntax

```swift
+ (void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

#### Example

```swift
ACPCore.setLogLevel(ACPMobileLogLevel.verbose);
```

{% endtab %}

{% endtabs %}



{% tabs %}

{% tab title="Android" %}

#### Java

### getLogLevel

#### Syntax

```java
public static LoggingMode getLogLevel()
```

#### Example

```java
LoggingMode mode = MobileCore.getLogLevel();
```

{% endtab %}

{% tab title="Objective-C" %}

#### Objective-C

### getLogLevel

#### Syntax

```objective-c
+ (ACPMobileLogLevel) logLevel;
```

#### Example

```
var logLevel:ACPMobileLogLevel = [ACPCore logLevel];
```

{% endtab %}

{% tab title="Swift" %}

#### Swift

### getLogLevel

#### Syntax

```swift
+ (ACPMobileLogLevel) logLevel;
```

#### Example

```swift
let logLevel:ACPMobileLogLevel = ACPCore.logLevel();
```

{% endtab %}

{% endtabs %}



{% tabs %}

{% tab title="Android" %}

#### Java

The `MobileCore` logging APIs use the `android.util.Log` APIs to log message to Android.

- `MobileCore.logTrace` calls `android.util.Log.v`
- `MobileCore.logDebug` calls `android.util.Log.d`
- `MobileCore.logWarning` calls `android.util.Log.w`
- `MobileCore.logError` calls `android.util.Log.e`

### logTrace

### logDebug

### logWarning

### logError

#### Syntax

```java
public static void logTrace(final String tag, final String message)
public static void logDebug(final String tag, final String message)
public static void logWarning(final String tag, final String message)
public static void logError(final String tag, final String message)
```

#### Example

```java
MobileCore.logDebug("MyActivity", "Debug message.");
```

{% endtab %}

{% tab title="Objective-C" %}

#### Objective-C

### log

#### Syntax

```objective-c
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

#### Example

```objective-c
[ACPCore log: ACPMobileLogLevelDebug, tag:@"source", message:@"debug message"];
```

{% endtab %}

{% tab title="Swift" %}

#### Swift

### log

#### Syntax

```swift
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

#### Example

```swift
ACPCore.log(ACPMobileLogLevel.debug, "source", "debug message");
```

{% endtab %}

{% endtabs %}

## Additional Information

* What is [context data](https://marketing.adobe.com/resources/help/en_US/sc/implement/context_data_variables.html)?

