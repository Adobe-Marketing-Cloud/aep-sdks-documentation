# Set up tracking

You can use the user actions APIs below to measure your user’s engagement with your app.

Actions are events that occur in your app. Use this API to track and measure an action, where each action has one or more corresponding metrics that increment each time the event occurs. For example, you might call this API for each new subscription each time an article is viewed, or each time a level is completed.

This section shows you how to start tracking app screens and user actions. To view and report on this data in those respective solutions, set up [Analytics](../../using-mobile-extensions/adobe-analytics/) or other Experience Cloud solution extensions.

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

### Objective C

#### Syntax

```text
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

#### Example

```text
 [ACPCore trackAction:@"action name" data:@{@"key":@"value"}];
```

### Swift

#### Syntax

```text
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

#### Example

```swift
ACPCore.trackAction("action name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

#### Syntax

```jsx
trackAction(action?: String, contextData?: { string: string });
```

#### Example

```jsx
ACPCore.trackAction("action", {"mytest": "action"});
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

#### Syntax

```dart
Future<void> trackAction(String action, {Map<String, String> data});
```

#### Example

```dart
FlutterACPCore.trackAction("mytest",  data: {"mytest": "action"});J
```
{% endtab %}

{% tab title="Cordova" %}
## Javascript

#### Calling trackAction

```javascript
ACPCore.trackAction("cordovaAction", {"cordovaKey":"cordovaValue"}, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
## C\#

#### Calling TrackAction

```csharp
var contextData = new Dictionary<string, string>();
contextData.Add("key", "value");
ACPCore.TrackAction("action name", contextData);
```
{% endtab %}

{% tab title="Xamarin" %}
## C\#

#### Calling TrackAction

**iOS**

```csharp
var data = new NSMutableDictionary<NSString, NSString>
{
  ["key"] = new NSString("value")
};
ACPCore.TrackAction("action", data);
```

**Android**

```csharp
var data = new Dictionary<string, string>();
data.Add("key", "value");
ACPCore.TrackAction("action", data);
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

### Objective C

#### Syntax

```text
 + (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

#### Example

```text
 [ACPCore trackState:@"state name" data:@{@"key":@"value"}];
```

### Swift

#### Syntax

```text
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

#### Example

```swift
ACPCore.trackState("state name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

#### Syntax

```jsx
trackState(state?: String, contextData?: { string: string });
```

#### Example

```jsx
ACPCore.trackState("state", {"mytest": "state"});
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

#### Syntax

```dart
Future<void> trackState(String state, {Map<String, String> data});
```

#### Example

```dart
FlutterACPCore.trackState("state",  data: {"mytest": "state"});
```
{% endtab %}

{% tab title="Cordova" %}
## Javascript

#### Calling track state

```javascript
ACPCore.trackState("cordovaState", {"cordovaKey":"cordovaValue"}, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
## C\#

#### Calling TrackState

```csharp
var dict = new Dictionary<string, string>();
dict.Add("key", "state value");
ACPCore.TrackState("state", dict);
```
{% endtab %}

{% tab title="Xamarin" %}
## C\#

#### Calling TrackState

**iOS**

```csharp
var data = new NSMutableDictionary<NSString, NSString>
{
  ["key"] = new NSString("value")
};
ACPCore.TrackState("state", data);
```

**Android**

```csharp
var data = new Dictionary<string, string>();
data.Add("key", "value");
ACPCore.TrackState("state", data);
```
{% endtab %}
{% endtabs %}

For more information, see [Mobile Core API Reference](../../using-mobile-extensions/mobile-core/mobile-core-api-reference.md).

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://helpx.adobe.com/contact/enterprise-support.ec.html) for immediate assistance

