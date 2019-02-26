# Mobile Core API Reference

# Application reference

When building Android applications, the `android.app.Application` reference must be passed to the Mobile SDK, which allows the Mobile SDK to access the `android.app.Context` and monitor the lifecycle of the Andorid application.

{% hint style="warning" %}

Android applications must call `MobileCore.setApplication()` before calling any other Mobile SDK API.

{% endhint %}

{% tabs %}

{% tab title="Android" %}

#### Java

### setApplication

#### Syntax

```java
public static void setApplication(final Application app)
```

#### Example

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

#### Java

### getApplication

{% hint style="warning" %}

`MobileCore.getApplication` might return `null` if the Application object was destroyed or if `MobileCore.setApplication` was not previously called.

{% endhint %}

#### Syntax

```java
public static Application getApplication()
```

#### Example

```java
Application app = MobileCore.getApplication();
if (app != null) {
    ...
}
```

{% endtab %}

{% endtabs %}



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

## Further Reading

* What is [context data](https://marketing.adobe.com/resources/help/en_US/sc/implement/context_data_variables.html)?

