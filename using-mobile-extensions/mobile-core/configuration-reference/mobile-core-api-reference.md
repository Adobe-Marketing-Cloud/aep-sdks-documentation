# Mobile Core API Reference

## Track app actions

Actions are events that occur in your app. Use this API to track and measure an action. Each action has one or more corresponding metrics that are incremented each time the event occurs. For example, you might call this API for each new subscription each time an article is viewed, or each time a level is completed.

{% hint style="warning" %}
You must call this API when an event that you want to track, occurs. In addition to the action name, you may send additional context data with each track action call. 
{% endhint %}

{% hint style="info" %}
If you have the **Analytics** extension setup, this method will send an Analytics action tracking hit along with the optional context data you provide.
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

States represent screens or views in your app. Each time a new state is displayed in your application, for example, when a user navigates from the home page to the news feed, this API may be called.. This method sends an Analytics state tracking hit with optional context data.

{% hint style="info" %}
If you have the **Analytics** extension setup, this API will increment page views and an Analytics state tracking hit along with the optional context data you provide.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

 In Android, trackState is typically called each time a new Activity is loaded

### trackState <a id="trackstate"></a>

#### **Syntax** <a id="syntax-1"></a>

```text
public static void trackState(final String state, final Map<String, String> contextData)
```

#### Example <a id="example-1"></a>

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

This API enables the SDK to collect sensitive or PII data. 

{% hint style="warning" %}
While this API enables the collection of sensitive data, no data is actually sent to any Adobe endpoint or 3rd party endpoint. To send the data to an endpoint, you may use a postback of PII type.
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

If the **Analytics** extension is enabled in your SDK, the collection of this launch data will result in an Analytics request being sent. Other extensions in the SDK might use the collected data, for example, as a rule condition for an In-App Message. {% endhint %}

{% tabs %} {% tab title="Android" %}

Coming soon

{% endtab %}

{% tab title="iOS" %}

#### Objective-C

This method should be called to support the following use cases:

- Tracking Deep Link click-throughs
  - From `application:didFinishLaunchingWithOptions`
  - Extract `userInfo` from `UIApplicationLaunchOptionsURLKey`
- Tracking Push Message click-through
  - From `application:didReceiveRemoteNotification:fetchCompletionHandler:`

### collectLaunchInfo

#### Syntax

```objective-c
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

#### Example

```objective-c
 [ACPCore collectLaunchInfo:launchOptions];
```

#### Swift

This method should be called to support the following use cases:

- Tracking Deep Link click-throughs
  - From `application(_:didFinishLaunchingWithOptions:)`
  - Extract `userInfo` from `url: UIApplication.LaunchOptionsKey`
- Tracking Push Message click-through
  - From `application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`

### collectLaunchInfo

#### Syntax

```swift
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

#### Example

```swift
ACPCore.collectLaunchInfo(userInfo)
```

{% endtab %} {% endtabs %}

## Further Reading

* What is [context data](https://marketing.adobe.com/resources/help/en_US/sc/implement/context_data_variables.html)?

