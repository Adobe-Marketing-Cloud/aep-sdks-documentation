# Project Griffon SDK API Reference

## startSession

The `startSession` API needs to be called to begin a Project Griffon session. When called, SDK displays a PIN authentication overlay to begin a session.

{% hint style="info" %}
You may call this API when the app launches with a url \(see code snippet below for sample usage\)
{% endhint %}

{% tabs %}
{% tab title="Android" %}
This API is optional for Android.

With the latest Project Griffon SDK extensions, Android does not require this API to be called. When the `registerExtension` API is called, Project Griffon registers the app lifecycle handlers which automatically pick up any deep links and use them to start the session.

### Java

### Syntax

```java
public static void startSession(final String url)
```

### Example

```java
 Griffon.startSession(url);
```
{% endtab %}

{% tab title="iOS" %}
### Objective-C

### Syntax

```objectivec
+ (void) startSession: (NSURL* _Nonnull) url;
```

### Example

```objectivec
- (BOOL)application:(UIApplication *)app openURL:(nonnull NSURL *)url options:(nonnull NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options {
    [ACPGriffon startSession:url];
    return false;
}
```

### Swift

### Example

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    do {
        ACPGriffon.startSession(url)
        return false
    }
}
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

### Syntax

```dart
static Future<void> startSession(String url);
```

### Example

```dart
FlutterGriffon.startSession(url);
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

### Syntax

```jsx
ACPGriffon.startSession(url, success, error);
```

* _url_ _\(String\)_ is the griffon session url.
* _success_ is a callback which indicates if the `startSession` API was executed without errors.
* _error_ is a callback containing error information if the `startSession` API was executed with errors.

### Example

```jsx
ACPGriffon.startSession(url, function(handleCallback) {
  console.log("AdobeExperenceSDK: Griffon session start successful: " + handleCallback);
}, function(handleError) {
  console.log("AdobeExperenceSDK: Failed to start griffon session: " + handleError);
});
```
{% endtab %}

{% tab title="Xamarin" %}

### C#

#### iOS Syntax

```c#
public static void StartSession (NSUrl url);
```

- _url_ _\(NSUrl\)_ is the Griffon session url.

#### Android Syntax

```c#
public unsafe static void StartSession (string url);
```

- _url_ _\(string\)_ is the Griffon session url.

#### iOS Example

```c#
NSUrl url = new NSUrl("session url");
ACPGriffon.StartSession(url);
```

#### Android Example

```c#
ACPGriffon.StartSession("session url");
```

### {% endtab %}

{% endtabs %}

## endSession

You can end a session in the app interface by pressing the floating indicator and selecting **Disconnect**. You can also programmatically close an active session by using the following API.

This API ends the active session and ensures that no data is sent to a Project Griffon session.

{% tabs %}
{% tab title="Android" %}
### Java

```java
Griffon.endSession()
```
{% endtab %}

{% tab title="iOS" %}
### Objective-C

### Syntax

```objectivec
+ (void) endSession;
```

### Example

```objectivec
[ACPGriffon endSession];
```

### Swift

### Example

```swift
ACPGriffon.endSession()
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

### Syntax

```dart
static Future<void> endSession();
```

### Example

```dart
FlutterGriffon.endSession();
```
{% endtab %}
{% endtabs %}

## sendEvent

You may send custom events from the app to Project Griffon using the following API. Custom events can help you inspect information from the app such as the API and network responses, foreground and background activity, asset and media downloads, performance metrics, timed processes, app startup times, or screen load times.

{% tabs %}
{% tab title="Android" %}
### Java

### Syntax

The follow syntax shows you how to use the sendEvent API:

```java
public static void sendEvent(final GriffonEvent event);
```

The following syntax shows you how to create a Griffon event:

```java
public GriffonEvent(final String vendor, final String type, final Map<String, Object> payload)
```

### Example

The following example shows you how to send a custom event that measures the download time of an asset’s download activity in the app.

```java
final Map<String, Object> eventPayload = new HashMap<>();
eventPayload.put("time", downloadTime);
eventPayload.put("size", data.length());

// create and send the Griffon event
final GriffonEvent event = new GriffonEvent("com.adobe.myapp", "download info", eventPayload);
Griffon.sendEvent(newEvent);
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

### Syntax

The follow syntax shows you how to use the sendEvent API:

```dart
static Future<void> sendEvent(String vendor, String type, Map payload);
```

### Example

The following example shows you how to send a custom event that measures the download time of an asset’s download activity in the app.

```dart
// create and send the Griffon event
FlutterGriffon.sendEvent("com.adobe.myapp", "download info", {"time": downloadTime, "size": data.length()});
```
{% endtab %}
{% endtabs %}

