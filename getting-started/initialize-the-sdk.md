# Track events

The SDK provides three event tracking APIs to log events for reporting, segmentation, and various other data collection use cases:

1. [Send events to Edge Network](initialize-the-sdk.md#send-events-to-edge-network) \(requires Edge Network extension\)
2. [Track user actions](initialize-the-sdk.md#track-user-actions) \(requires Adobe Analytics extension\)
3. [Track app states and screens](initialize-the-sdk.md#track-app-states-and-screens) \(requires Adobe Analytics extension\)

## Send events to Edge Network

{% hint style="info" %}
This step requires knowledge of Experience Data Model \(XDM\) in Adobe Experience Platform. For more information about XDM, please read the [XDM documentation](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html).
{% endhint %}

The Edge Network extension provides an API to send an `ExperienceEvent` to Edge Network. An Experience Event is an object that contains data conforming to the XDM `ExperienceEvent` schema definition in Adobe Experience Platform.

In the following reference examples, you'll create an `ExperienceEvent` and then send it using the `sendEvent` API.

Additionally, you'll need to add the `Environment Details` field group and create a custom field group for product reviews that contain the following fields:

* productSku
* rating
* ratingText
* reviewerId

### Create an Experience Event

{% tabs %}
{% tab title="Android" %}
### Java

```text
Map<String, Object> reviewXdmData = new HashMap<>();
reviewXdmData.put("productSku", "demo123");
reviewXdmData.put("rating", 5);
reviewXdmData.put("reviewText", "I love this demo!");
reviewXdmData.put("reviewerId", "Anonymous user");

Map<String, Object> xdmData = new HashMap<>();
xdmData.put("eventType", "MyFirstXDMExperienceEvent");
xdmData.put(_yourTenantId, reviewXdmData);

ExperienceEvent experienceEvent = new ExperienceEvent.Builder()
                .setXdmSchema(xdmData)
                .build();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

```swift
var xdmData : [String: Any] = [:]
xdmData["eventType"] = "MyFirstXDMExperienceEvent"
xdmData[_yourTenantId] = ["productSku": "demo123",
                          "rating": 5,
                          "reviewText": "I love this demo!",
                          "reviewerId": "Anonymous user"]
let experienceEvent = ExperienceEvent(xdm: xdmData)
```

### Objective-C

```text
NSDictionary<NSString*, NSObject*>* xdmData;
[xdmData setValue:@"MyFirstXDMExperienceEvent" forKey:@"eventType"];
[xdmData setValue:@{@"productSku": @"demo123",
                    @"rating": @5,
                    @"reviewText": @"I love this demo!",
                    @"reviewerId": @"Anonymous user"}
                      forKey:_yourTenantId];
AEPExperienceEvent *experienceEvent = [[AEPExperienceEvent alloc] initWithXdm:xdmData data:nil datasetIdentifier:nil];
```
{% endtab %}
{% endtabs %}

### Send the Experience Event to Edge Network

Use the Adobe Experience Platform Edge Mobile Extension to send the Experience Event created in the previous step.

{% tabs %}
{% tab title="Android" %}
### Java

```text
Edge.sendEvent(experienceEvent, null);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

```swift
Edge.sendEvent(experienceEvent: experienceEvent)
```

### Objective-C

```text
[AEPMobileEdge sendExperienceEvent:event completion:nil];
```
{% endtab %}
{% endtabs %}

## Track user actions \(for Adobe Analytics\)

This section shows you how to start track user actions in your mobile app. To view and report on this data in those respective solutions, set up [Adobe Analytics](../using-mobile-extensions/adobe-analytics/) or another Experience Cloud solution extensions.

Actions are events that occur in your app. Use this API to track and measure an action, where each action has one or more corresponding metrics that increment each time the event occurs. For example, you might call this API for every new subscription, every time an article is viewed, or every time a level is completed.

{% hint style="warning" %}
You must call this API when an event that you want to track occurs. In addition to the action name, you can send additional context data with each track action call.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### trackAction <a id="trackaction"></a>

#### Java <a id="java"></a>

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

{% tab title="iOS (AEP 3.x)" %}

### trackAction <a id="AEPExample"></a>

#### Swift

**Syntax**

```swift
static func track(action: String?, data: [String: Any]?)
```

**Example**

```swift
MobileCore.track(action: "actionName", data: ["key": "value"])
```

#### Objective-C

**Syntax**

```swift
@objc(trackAction:data:)
static func track(action: String?, data: [String: Any]?)
```

**Example**

```objectivec
[AEPMobileCore trackAction:@"action name" data:@{@"key": @"value"}];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### trackAction <a id="ACPExample"></a>

#### Objective-C

**Syntax**

```objectivec
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

**Example**

```objectivec
 [ACPCore trackAction:@"action name" data:@{@"key":@"value"}];
```

### Swift

**Syntax**

```objectivec
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) data;
```

**Example**

```swift
ACPCore.trackAction("action name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Syntax**

```jsx
trackAction(action?: String, contextData?: { string: string });
```

**Example**

```jsx
ACPCore.trackAction("action", {"mytest": "action"});
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

**Syntax**

```dart
Future<void> trackAction(String action, {Map<String, String> data});
```

**Example**

```dart
FlutterACPCore.trackAction("mytest",  data: {"mytest": "action"});J
```
{% endtab %}

{% tab title="Cordova" %}
### Javascript

#### Calling trackAction

```javascript
ACPCore.trackAction("cordovaAction", {"cordovaKey":"cordovaValue"}, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
### C\#

#### Calling `TrackAction`

```csharp
var contextData = new Dictionary<string, string>();
contextData.Add("key", "value");
ACPCore.TrackAction("action name", contextData);
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

#### Calling `TrackAction`

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

## Track app states and screens \(for Adobe Analytics\)

States represent screens or views in your app. The `trackState` method is called every time a new state is displayed in your application. For example, this method would be called when a user navigates from the home page to the news feed. This method also sends an Adobe Analytics state-tracking hit with optional context data.

{% tabs %}
{% tab title="Android" %}
### trackState <a id="trackstate"></a>

On Android, `trackState` is typically called each time a new activity is loaded.

#### Java

**Syntax**

```java
public static void trackState(final String state, final Map<String, String> contextData)
```

**Example**

```java
Map<String, String> additionalContextData = new HashMap<String, String>();         
additionalContextData.put("customKey", "value");         
MobileCore.trackState("homePage", additionalContextData);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### trackState <a id="aepExample"></a>

#### Swift

**Syntax**

```swift
static func track(state: String?, data: [String: Any]?) 
```
**Example**

```swift
MobileCore.track(state: "state name", data: ["key": "value"])
```

#### Objective-C

**Syntax**

```swift
@objc(trackState:data:)
static func track(state: String?, data: [String: Any]?) 
```
**Example**

```objectivec
[AEPMobileCore trackState:@"state name" data:@{@"key": @"value"}];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### trackState <a id="acpExample"></a>

#### Objective-C

**Syntax**

```text
 + (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

**Example**

```text
 [ACPCore trackState:@"state name" data:@{@"key":@"value"}];
```

### Swift

**Syntax**

```text
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) data;
```

**Example**

```swift
ACPCore.trackState("state name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Syntax**

```jsx
trackState(state?: String, contextData?: { string: string });
```

**Example**

```jsx
ACPCore.trackState("state", {"mytest": "state"});
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

**Syntax**

```dart
Future<void> trackState(String state, {Map<String, String> data});
```

**Example**

```dart
FlutterACPCore.trackState("state",  data: {"mytest": "state"});
```
{% endtab %}

{% tab title="Cordova" %}
### Javascript

#### Calling `trackState`

```javascript
ACPCore.trackState("cordovaState", {"cordovaKey":"cordovaValue"}, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
### C\#

#### Calling `TrackState`

```csharp
var dict = new Dictionary<string, string>();
dict.Add("key", "state value");
ACPCore.TrackState("state", dict);
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

#### Calling `TrackState`

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

For more information, see the [Mobile Core API Reference](../foundation-extensions/mobile-core/mobile-core-api-reference.md).

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://experienceleague.adobe.com/?support-solution=General#support) for immediate assistance

