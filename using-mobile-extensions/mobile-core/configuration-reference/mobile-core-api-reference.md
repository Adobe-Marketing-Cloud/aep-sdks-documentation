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

{% tab title="Objective-C" %}
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
{% endtab %}

{% tab title="Swift" %}
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

 In Android, trackState is typically called each time a new activity is loaded

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

{% tab title="Objective-C" %}
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
{% endtab %}

{% tab title="Swift" %}
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



## Collect launch information

You can provide the user info to the SDK from various launch points in your application. 

{% hint style="info" %}

If **Analytics** extension is enabled in your SDK, the collection of this launch data will result in an Analytics request being sent. Other extensions in the SDK might use the collected data, for example, as a rule condition for an In-App Message.
{% endhint %}

{% tabs %}
{% tab title="Android" %}

#### Java

In Android, you can collect data from the Activity or the context to be used later by the SDK.

The `collectLaunchInfo` API marshals the Activity instance and extracts the intent data or extras. It should be called to support the following use cases:

- Tracking Deep Link click-throughs
  - Update `AndroidManifest.xml` to support intent-filter in the activity with the intended action and type of data.
  - Handle the intent in the activity.
  - Pass the Activity with deepLink intent to SDK in `collectLaunchInfo`
- Tracking Push Message click-through
  - Push message data must be added to the Intent used to open target activity on click-through.
  - The data can be added in intent extras which is then collected by SDK when the target activity is passed in `collectLaunchInfo`.
- Tracking Local Notification click-through
  - Add manifest-declared broadcast receiver ` <receiver android:name=".LocalNotificationHandler" />`  in your application.
  - Pass notifications activity reference in `collectLaunchInfo`. 

### collectLaunchInfo  <a id="collectLaunchInfo"></a>

#### **Syntax** <a id="syntax-2"></a>

```text
public static void collectLaunchInfo(Activity activity);
```

#### Example <a id="example-2"></a>

```text
@Override
protected void onResume() { 
	super.onResume();
	MobileCore.collectLaunchInfo(this);
	...
}
```

{% endtab %}

{% tab title="Objective-C" %}

#### Objective-C

This method should be called to support the following use cases:

- Tracking Deep Link click-throughs
  - From `application:didFinishLaunchingWithOptions`
  - Extract `userInfo` from `UIApplicationLaunchOptionsURLKey`
- Tracking Push Message click-through
  - From `application:didReceiveRemoteNotification:fetchCompletionHandler:` 

### collectLaunchInfo

#### Syntax

```objectivec
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

#### Example

```objectivec
 [ACPCore collectLaunchInfo:launchOptions];
```

{% endtab %}

{% tab title="Swift" %}

#### Swift

This method should be called to support the following use cases:

- Tracking Deep Link click-throughs
  - From `application(_:didFinishLaunchingWithOptions:)`
  - Extract `userInfo` from `url: UIApplication.LaunchOptionsKey`
- Tracking Push Message click-through
  - From `application(_:didReceiveRemoteNotification:fetchCompletionHandler:)` 

### collectLaunchInfo

#### Syntax

```objectivec
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

#### Example

```swift
ACPCore.collectLaunchInfo(userInfo)
```

{% endtab %}
{% endtabs %}

## Further Reading

* What is [context data](https://marketing.adobe.com/resources/help/en_US/sc/implement/context_data_variables.html)?

