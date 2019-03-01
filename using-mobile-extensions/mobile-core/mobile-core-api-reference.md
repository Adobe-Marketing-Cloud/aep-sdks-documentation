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


## Set Icons for local notification

Set the small and large icons that will be used for notifications that are created by the SDK. The small icon appears in the status bar and is the secondary image that is displayed shown when the user sees the complete notification in the notification center. The large icon will be the primary image that is displayed when the user sees the complete notification in the notification center.

{% hint style="info" %}
Those APIs are Android only.
{% endhint %}

#### Java


### setSmallIconResourceID

#### Syntax

```java
public static void setSmallIconResourceID(int resourceID) 
```

#### Example

```java
 MobileCore.setSmallIconResourceID(R.mipmap.ic_launcher_round);
```

### setLargeIconResourceID

#### Syntax

```java
public static void setLargeIconResourceID(int resourceID) 
```

#### Example

```java
 MobileCore.setLargeIconResourceID(R.mipmap.ic_launcher_round);
```

## Additional Information

* What is [context data](https://marketing.adobe.com/resources/help/en_US/sc/implement/context_data_variables.html)?

